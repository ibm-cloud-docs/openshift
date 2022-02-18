---

copyright:
  years: 2022, 2022
lastupdated: "2022-02-18"

keywords: openshift

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Pods in the `openshift-markeplace` namespace are in `ImagePullBackOff`
{: #ts-openshift-marketplace}
{: support}

**Infrastructure provider**:
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC


In VPC clusters with worker nodes in a VPC subnet that doesn't have a public gateway, the pods in the `openshift-markeplace` namespace show a state of `ImagePullBackOff` and cannot reach `Running` state.
{: tsSymptoms}


The images for these containers are hosted on a public image registry but the workers do not have access to the public internet, so the workers cannot to pull the image. The cluster still works, but these pods and the openshift marketplace does not work. If you run the `kubectl get pods` command, you get output such as:
{: tsCauses}

```sh
NAME                                    READY   STATUS             RESTARTS   AGE     IP               NODE         NOMINATED NODE   READINESS GATES
certified-operators-48dsc               0/1     ImagePullBackOff   0          4h6m    172.17.70.94     172.24.0.6   <none>           <none>
certified-operators-s7qtb               0/1     ImagePullBackOff   0          4h17m   172.17.70.77     172.24.0.6   <none>           <none>
community-operators-h7hl9               0/1     ImagePullBackOff   0          4h17m   172.17.70.78     172.24.0.6   <none>           <none>
community-operators-hc76f               0/1     ImagePullBackOff   0          4h6m    172.17.70.96     172.24.0.6   <none>           <none>
marketplace-operator-66c666bf74-gnltf   1/1     Running            0          4h43m   172.17.126.216   172.24.0.8   <none>           <none>
redhat-marketplace-tfwwp                0/1     ImagePullBackOff   0          82s     172.17.126.226   172.24.0.8   <none>           <none>
redhat-marketplace-zkvfc                0/1     ImagePullBackOff   0          4h6m    172.17.70.95     172.24.0.6   <none>           <none>
redhat-operators-pthhf                  0/1     ImagePullBackOff   0          67s     172.17.126.227   172.24.0.8   <none>           <none>
redhat-operators-rjvsp                  0/1     ImagePullBackOff   0          4h6m    172.17.70.93     172.24.0.6   <none>           <none>
```
{: screen}


You can fix this issue by disabling and mirroring these public images. For more information, see [Disabling and mirroring OperatorHub catalog source images](/docs/openshift?topic=openshift-operators#mirror-operatorhub).
{: tsResolve}
