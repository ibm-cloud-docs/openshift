---

copyright: 
  years: 2014, 2024
lastupdated: "2024-07-23"


keywords: openshift, kubernetes, affinity, taint, edge node, edge

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}





# Deploying the Sysdig agent on edge worker nodes
{: #edge-sysdig}

To allow the Sysdig agent pods to be deployed to your edge worker nodes, run the following `kubectl patch` command to update the `sysdig-agent` DaemonSet. This command applies the `NoExecute` toleration to the DaemonSet to ensure that the agent pods don't get evicted from the node.

```sh
kubectl patch ds sysdig-agent -n ibm-observe --type merge --type='json' -p='[{"op": "add", "path": "/spec/template/spec/tolerations/-", "value": {"operator": Exists, "effect": NoExecute}}]'
```
{: pre}

If you used pod labels such as `dedicated=edge`, you can also apply this label to any pods that you want to allow on your edge nodes.
{: tip}


