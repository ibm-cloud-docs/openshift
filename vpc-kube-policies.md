---

copyright: 
  years: 2014, 2022
lastupdated: "2022-03-03"

keywords: openshift, firewall, acl, acls, access control list, rules, security group

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Controlling traffic between pods with Kubernetes policies
{: #vpc-kube-policies}

You can use Kubernetes policies to control network traffic between pods in your cluster and to isolate app microservices from each other within a namespace or across namespaces.
{: shortdesc}

**Level of application**: Worker node host endpoint

**Default behavior**: No Kubernetes network policies exist by default in your cluster. By default, any pod has access to any other pod in the cluster. Additionally, any pod has access to any services that are exposed by the pod network, such as a metrics service, the cluster DNS, the API server, or any services that you manually create in your cluster.

**Use case**: Kubernetes network policies specify how pods can communicate with other pods and with external endpoints. Both incoming and outgoing network traffic can be allowed or blocked based on protocol, port, and source or destination IP addresses. Traffic can also be filtered based on pod and namespace labels. When Kubernetes network policies are applied, they are automatically converted into Calico network policies. The Calico network plug-in in your cluster enforces these policies by setting up Linux Iptables rules on the worker nodes. Iptables rules serve as a firewall for the worker node to define the characteristics that the network traffic must meet to be forwarded to the targeted resource.

If most or all pods don't require access to specific pods or services, and you want to ensure that pods by default can't access those pods or services, you can create a Kubernetes network policy to block ingress traffic to those pods or services.

For more information about how Kubernetes network policies control pod-to-pod traffic and for more example policies, see the [Kubernetes documentation](https://kubernetes.io/docs/concepts/services-networking/network-policies/){: external}.
{: tip}

## Isolate app services within a namespace
{: #services_one_ns}

The following scenario demonstrates how to manage traffic between app microservices within one namespace.
{: shortdesc}

An Accounts team deploys multiple app services in one namespace, but they need isolation to permit only necessary communication between the microservices over the public network. For the app `Srv1`, the team has front end, back end, and database services. They label each service with the `app: Srv1` label and the `tier: frontend`, `tier: backend`, or `tier: db` label.

![Use a network policy to manage cross-namespace traffic.](images/cs_network_policy_single_ns.png "Use a network policy to manage cross-namespace traffic"){: caption="Figure 1. Use a network policy to manage cross-namespace traffic" caption-side="bottom"}

The Accounts team wants to allow traffic from the front end to the back end, and from the back end to the database. They use labels in their network policies to designate which traffic flows are permitted between microservices.

First, they create a Kubernetes network policy that allows traffic from the front end to the back end:

```yaml
kind: NetworkPolicy
apiVersion: networking.k8s.io/v1
metadata:
  name: backend-allow
spec:
  podSelector:
    matchLabels:
      app: Srv1
      tier: backend
  ingress:
  - from:
    - podSelector:
        matchLabels:
          app: Srv1
          Tier: frontend
```
{: codeblock}

The `spec.podSelector.matchLabels` section lists the labels for the Srv1 back-end service so that the policy applies only _to_ those pods. The `spec.ingress.from.podSelector.matchLabels` section lists the labels for the Srv1 front-end service so that ingress is permitted only _from_ those pods.

Then, they create a similar Kubernetes network policy that allows traffic from the back end to the database:

```yaml
kind: NetworkPolicy
apiVersion: networking.k8s.io/v1
metadata:
  name: db-allow
spec:
  podSelector:
    matchLabels:
      app: Srv1
      tier: db
  ingress:
  - from:
    - podSelector:
        matchLabels:
          app: Srv1
          Tier: backend
```
{: codeblock}

The `spec.podSelector.matchLabels` section lists the labels for the Srv1 database service so that the policy applies only _to_ those pods. The `spec.ingress.from.podSelector.matchLabels` section lists the labels for the Srv1 back-end service so that ingress is permitted only _from_ those pods.

Traffic can now flow from the front end to the back end, and from the back end to the database. The database can respond to the back end, and the back end can respond to the front end, but no reverse traffic connections can be established.

## Isolate app services between namespaces
{: #services_across_ns}

The following scenario demonstrates how to manage traffic between app microservices across multiple namespaces.
{: shortdesc}

Services that are owned by different subteams need to communicate, but the services are deployed in different namespaces within the same cluster. The Accounts team deploys front end, back end, and database services for the app Srv1 in the accounts namespace. The Finance team deploys front end, back end, and database services for the app Srv2 in the finance namespace. Both teams label each service with the `app: Srv1` or `app: Srv2` label and the `tier: frontend`, `tier: backend`, or `tier: db` label. They also label the namespaces with the `usage: accounts` or `usage: finance` label.

![Use a network policy to manage cross-namepspace traffic.](images/cs_network_policy_multi_ns.png) "Use a network policy to manage cross-namespace traffic"){: caption="Figure 1. Use a network policy to manage cross-namespace traffic" caption-side="bottom"}

The Finance team's Srv2 needs to call information from the Accounts team's Srv1 back end. So the Accounts team creates a Kubernetes network policy that uses labels to allow all traffic from the finance namespace to the Srv1 back end in the accounts namespace. The team also specifies the port 3111 to isolate access through that port only.

```yaml
kind: NetworkPolicy
apiVersion: networking.k8s.io/v1
metadata:
  Namespace: accounts
  name: accounts-allow
spec:
  podSelector:
    matchLabels:
      app: Srv1
      Tier: backend
  ingress:
  - from:
    - NamespaceSelector:
        matchLabels:
          usage: finance
      ports:
        port: 3111
```
{: codeblock}

The `spec.podSelector.matchLabels` section lists the labels for the Srv1 back-end service so that the policy applies only _to_ those pods. The `spec.ingress.from.NamespaceSelector.matchLabels` section lists the label for the finance namespace so that ingress is permitted only _from_ services in that namespace.

Traffic can now flow from finance microservices to the accounts Srv1 back end. The accounts Srv1 back end can respond to finance microservices, but can't establish a reverse traffic connection.

In this example, all traffic from all microservices in the finance namespace is permitted. You can't allow traffic from specific app pods in another namespace because `podSelector` and `namespaceSelector` can't be combined.


