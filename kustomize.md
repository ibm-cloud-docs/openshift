---

copyright:
  years: 2023, 2024
lastupdated: "2024-10-10"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, node.js, js, java, .net, go, flask, react, python, swift, rails, ruby, spring boot, angular

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}




# Packaging apps for reuse in multiple environments with Kustomize
{: #kustomize}

As part of a [twelve-factor](https://12factor.net/){: external}, cloud-native app, you want to maintain `dev-to-prod` parity by setting up a continuous development and delivery pipeline that uses a common, version-controlled code base source. In your code base repositories, you store your Kubernetes resource configuration manifest files, often in YAML format. You can use the Kubernetes project [Kustomize](https://kustomize.io/){: external} both to standardize and customize your deployments across multiple environments.
{: shortdesc}

For example, you can set up a base `kustomization` YAML file to declare Kubernetes objects such as deployments and PVCs that are shared in your development, testing, and production environments. Next, you can set up separate `kustomization` YAML files that have customized configurations for each environment, such as more replicas in production than testing. These customized YAML files can then overlay, or build on, the shared base YAML file so that you can manage environments that are mostly identical except for a few overlay configuration differences that you source-control. For more information about Kustomize such as a glossary and FAQs, check out the [Kustomize docs](https://kubectl.docs.kubernetes.io/references/kustomize/){: external}.

Before you begin: [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

To set up configuration files with Kustomize:
1. [Install the `kustomize` tool](https://kubectl.docs.kubernetes.io/installation/kustomize/){: external}.
    - For macOS, you can use the `brew` package manager.
        ```sh
        brew install kustomize
        ```
        {: pre}

    - For Windows, you can use the `chocolatey` package manager.
        ```sh
        choco install kustomize
        ```
        {: pre}

2. Create a directory for your app in a version control system, such as Git.
    ```sh
    git init ~/<my_app>
    ```
    {: pre}

3. Create your repo structure for your `kustomize` [`base`](https://kubectl.docs.kubernetes.io/references/kustomize/glossary/#base){: external} directory, [`overlay`](https://kubectl.docs.kubernetes.io/references/kustomize/glossary/#overlay){: external} directory, and environment directories such as staging and production. In the subsequent steps, you set up these repos for use with `kustomize`.
    ```sh
    mkdir -p ~/<my_app>/base &&
    mkdir -p ~/<my_app>/overlay &&
    mkdir -p ~/<my_app>/overlay/staging &&
    mkdir -p ~/<my_app>/overlay/prod
    ```
    {: pre}

    Example repo structure
    ```sh
    .
    ├── base
    └── overlay
        ├── prod
        └── staging
    ```
    {: screen}

4. Set up the `base` repo.
    1. Navigate to the base repo.
        ```sh
        cd ~/<my_app>/base
        ```
        {: pre}

    2. Create an initial set of Kubernetes configuration YAML files for your app deployment. You might use the `wasliberty` [YAML example](/docs/openshift?topic=openshift-app#yaml-example) to create a deployment, service, config map, and persistent volume claim.
    3. Create a [`kustomization` file](https://github.com/kubernetes-sigs/kustomize#1-make-a-kustomization-file){: external} that specifies the base configuration to be applied across environments. The `kustomization` file must include the list of Kubernetes resource configuration YAMLs that are stored in the same `base` repo. In the `kustomization` file, you can also add configurations that apply to all the resource YAMLs in the base repo, such as a prefix or suffix that is appended to all the resource names, a label, the existing namespace all the resources are created in, secrets, configmaps, and more.
        ```yaml
        apiVersion: kustomize.config.k8s.io/v1beta1
        kind: Kustomization
        namespace: wasliberty
        namePrefix: kustomtest-
        nameSuffix: -v2
        commonLabels:
          app: kustomized-wasliberty
        resources:
        - deployment.yaml
        - service.yaml
        - pvc.yaml
        - configmap.yaml
        - secret.yaml
        ```
        {: codeblock}

        The names of the `resources` YAMLs must match the names of the other files in the `base` repo. You might include multiple configurations in the same file, but in the example, the configurations are separate files such as `deployment.yaml`, `service.yaml`, and `pvc.yaml`.

    4. Build your resource YAML files with the configurations that you defined in the `kustomization` base YAML file. The resources are built by combining the configurations in the `kustomization` and resource YAMLs together. The combined YAML files are returned in `stdout` in the output. Use this same command to build any subsequent changes that you make to the `kustomization` YAML, such adding a label.
        ```sh
        kustomize build
        ```
        {: pre}

5. Set up your overlay repo with unique `kustomization` YAML files for each of your environments, such as staging and prod.
    1. In the staging repo, create a `kustomization.yaml` file. Add any configurations that are unique to staging, such as a label, image tag, or YAML for a new component that you want to test out.
        ```yaml
        apiVersion: kustomize.config.k8s.io/v1beta1
        kind: Kustomization
        namePrefix: staging-
        commonLabels:
          env: staging
          owner: TeamA
        bases:
        - ../../base
        patchesStrategicMerge:
        - configmap.yaml
        - new_staging_resource.yaml
        resources:
        - new_staging_resource.yaml
        ```
        {: codeblock}
        
        | Component | Description |
        | ----- | ---------- |
        | `namePrefix` | Specify a prefix to attach to the name of each resource that you want to create with your staging `kustomization` file, such as `staging-`. |
        | `commonLabels` | Add labels that are unique to the staging objects, such as the staging environment and responsible team. |
        | `bases` | Add a relative path to a directory or URL to a remote repo that contains a base `kustomization` file. In this example, the relative path points to the base `kustomization` file in the `base` repo that you previously created. This field is required for an overlay `kustomization`. |
        | `patchesStrategicMerge` | List the resource configuration YAML files that you want to merge to the base `kustomization`. You must also add these files to the same repo as the `kustomization` file, such as `overlay/staging`. These resource configuration files can contain small changes that are merged to the base configuration files of the same name as a patch. The resource gets all the components that are in the `base` configuration file, plus any additional components that you specify in the `overlay` configuration file. If the configuration is a new file that is not in the base, you must also add the file name to the `resources` field. |
        | `resources` | List any resource configuration YAML files that are unique to the staging repo and not included in the base repo. Include these files in the `patchesStrategicMerge` field also, and add them to the same repo as the `kustomization` file, such as `overlay/staging`. |
        | Other possible configurations | For more configurations that you might add to your file, see the [Make a `kustomization` file](https://github.com/kubernetes-sigs/kustomize#1-make-a-kustomization-file){: external}. |
        {: caption="Understanding YAML components" caption-side="bottom"}

    2. Build your staging overlay configuration files.
        ```sh
        kustomize build overlay/staging
        ```
        {: pre}

    3. Repeat these steps to create your prod overlay `kustomization` and other configuration YAML files. For example, you might increase the number of replicas in your `deployment.yaml` so that your prod environment can handle more user requests.
    4. Review your `kustomize` repo structure to make sure that it includes all the YAML configuration files that you need. The structure might look similar to the following example.
        ```sh
        ├── base
        │   ├── configmap.yaml
        │   ├── deployment.yaml
        │   ├── kustomization.yaml
        │   ├── pvc.yaml
        │   ├── secret.yaml
        │   └── service.yaml
        └── overlay
            ├── prod
            │   ├── deployment.yaml
            │   ├── kustomization.yaml
            │   └── new_prod_resource.yaml
            └── staging
                ├── configmap.yaml
                ├── kustomization.yaml
                └── new_staging_resource.yaml
        ```
        {: screen}

6. Apply the Kubernetes resources for the environment that you want to deploy. The following example uses the staging repo.
    1. Navigate to the staging overlay directory. If you did not build your resources in the previous step, create them now.
        ```sh
        cd overlay/staging && kustomize build
        ```
        {: pre}

    2. Apply the Kubernetes resources to your cluster. Include the `-k` option and the directory where the `kustomization` file is located. For example, if you are already in the staging directory, include `../staging` to mark the path to the directory.
        ```sh
        oc apply -k ../staging
        ```
        {: pre}

        Example output
        ```sh
        configmap/staging-kustomtest-configmap-v2 created
        secret/staging-kustomtest-secret-v2 created
        service/staging-kustomtest-service-v2 created
        deployment.apps/staging-kustomtest-deployment-v2 created
        job.batch/staging-pi created
        persistentvolumeclaim/staging-kustomtest-pvc-v2 created
        ```
        {: screen}
        
    3. Check to make sure that the staging-unique changes are applied. For example, if you added a `staging-` prefix, the pods and other resources that are created include this prefix in their name.
        ```sh
        oc get -k ../staging
        ```
        {: pre}

        Example output
        ```sh
        NAME                                        DATA   AGE
        configmap/staging-kustomtest-configmap-v2   2      90s

        NAME                                  TYPE     DATA   AGE
        secret/staging-kustomtest-secret-v2   Opaque   2      90s

        NAME                                    TYPE       CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
        service/staging-kustomtest-service-v2   NodePort   172.21.xxx.xxx   <none>        9080:30200/TCP   90s

        NAME                                               READY   UP-TO-DATE   AVAILABLE   AGE
        deployment.apps/staging-kustomtest-deployment-v2   0/3     3            0           91s

        NAME                   COMPLETIONS   DURATION   AGE
        job.batch/staging-pi   1/1           41s        2m37s

        NAME                                              STATUS    VOLUME   CAPACITY   ACCESS MODES   STORAGECLASS       AGE
        persistentvolumeclaim/staging-kustomtest-pvc-v2   Pending                                      ibmc-file-bronze   90s
        ```
        {: screen}

    4. Repeat these steps for each environment that you want to build.
7. **Optional**: Clean up your environment by removing all the resources that you applied with Kustomize.
    ```sh
    oc delete -k <directory>
    ```
    {: pre}

    Example output

    ```sh
    configmap "staging-kustomtest-configmap-v2" deleted
    secret "staging-kustomtest-secret-v2" deleted
    service "staging-kustomtest-service-v2" deleted
    deployment.apps "staging-kustomtest-deployment-v2" deleted
    job.batch "staging-pi" deleted
    persistentvolumeclaim "staging-kustomtest-pvc-v2" deleted
    ```
    {: screen}
    
