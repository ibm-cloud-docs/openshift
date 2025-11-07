---

copyright: 
  years: 2014, 2025
lastupdated: "2025-11-07"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, kubernetes, node scaling, ca, autoscaler, gpu, hpa

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}

# Setting up horizontal pod autoscaling on GPU worker nodes
{: #cluster-scaling-hpa-gpu}

Review the following steps to enable horizontal pod autoscaling on your GPU worker nodes.


Why horizontal pod autoscaling?
:   You might want to configure horizontal pod autoscaling to scale the number of pods when the workload consumes more or less than a certain amount of GPU. Because GPUs are an expensive resource you might not want workloads to be run at the fullest capacity long periods of time. Instead, you can scale pods or up down based on the running workload in the cluster.

## Prerequisites
{: #hpa-gpu-prereqs}

To configure HPA, the following components must be installed on your cluster.
- NVIDIA Data Center GPU Manager (DCGM) exporter to gather GPU metrics in Kubernetes. The DCGM exporter exposes GPU metrics for Prometheus which can be visualized using Grafana.
- Prometheus and the Prometheus adapter to generate custom metrics.

1. [Install the NVIDIA GPU Operator](https://docs.nvidia.com/datacenter/cloud-native/openshift/latest/steps-overview.html){: external}


1. Install Prometheus.
    ```sh
    helm install prom-stack prometheus-community/kube-prometheus-stack -f ~/ca-prom-val.yaml
    ```
    {: pre}

    ```sh
    cat ~/ca-prom-val.yaml
    ```
    {: pre}

    ```yaml
    prometheus:
        prometheusSpec:
            additionalScrapeConfigs:
            - job_name: gpu-metrics
                scrape_interval: 1s
                metrics_path: /metrics
                scheme: http
                kubernetes_sd_configs:
                - role: endpoints
                    namespaces:
                        names:
                        - nvidia-gpu-operator
                relabel_configs:
                - source_labels: [__meta_kubernetes_endpoints_name]
                    action: drop
                    regex: .*-node-feature-discovery-master
                - source_labels: [__meta_kubernetes_pod_node_name]
                    action: replace
                    target_label: kubernetes_node
    ```
    {: screen}

1. Get the Prometheus service details.
    ```sh
    oc get svc
    ```
    {: pre}

1. Install the Prometheus adapter.
    ```sh
    helm upgrade --install prometheus-adapter prometheus-community/prometheus-adapter --set prometheus.url="http://prom-stack-kube-prometheus-prometheus.default.svc.cluster.local"
    ```
    {: pre}


## Setting up HPA
{: #hpa-gpu-setup}

Complete the following steps to create a deployment that uses HPA.

1. Create a deployment.
    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
        name: cuda-test
        labels:
            app: cuda-test
    spec:
        selector:
            matchLabels:
                app: cuda-test
        template:
            metadata:
                labels:
                    app: cuda-test
            spec:
                containers:
                - name: cuda-test-main
                    image: "k8s.gcr.io/cuda-vector-add:v0.1"
                    command: ["bash", "-c", "for (( c=1; c<=5000; c++ )); do ./vectorAdd; done"]
                    resources:
                        limits:
                            nvidia.com/gpu: 1
    ```
    {: codeblock}

1. Create a `HorizontalPodAutoscaler` resource.
    ```yaml
    kind: HorizontalPodAutoscaler
    apiVersion: autoscaling/v2
    metadata:
        name: cuda-hpa
        namespace: default
    spec:
        scaleTargetRef:
            apiVersion: apps/v1
            kind: Deployment
            name: cuda-test
        minReplicas: 1
        maxReplicas: 3
        metrics:
            - type: Pods
                pods:
                    metric:
                        name: DCGM_FI_DEV_GPU_UTIL     #the metric you want to use for autoscaling
                    target:
                        type: AverageValue
                        averageValue: '5'
    ```
    {: codeblock}


1. Run the following commands to review the results.
    ```sh
    oc get pods | grep cuda
    ```
    {: pre}

    ```sh
    cuda-test-d987464bf-brd48                                1/1     Running   0          4m19s
    cuda-test-d987464bf-gsx82                                0/1     Pending   0          4m19s
    cuda-test-d987464bf-zstzs                                1/1     Running   0          7m35s
    ```
    {: screen}


    There was 1 replica that was scaled up to 3 as the workload resource increased.
    ```sh
    Min replicas:       1
    Max replicas:       3
    Deployment pods:    3 current / 3 desired
    Events:
    Type    Reason             Age   From                       Message
    ----    ------             ----  ----                       -------
    Normal  SuccessfulRescale  50s   horizontal-pod-autoscaler  New size: 3; reason: pods metric DCGM_FI_DEV_GPU_UTIL above target
    ``` 
    {: screen}
