---

copyright:
  years: 2014, 2021
lastupdated: "2021-09-28"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift
content-type: troubleshoot

---


{{site.data.keyword.attribute-definition-list}}
  

# Why are pods in a `CrashLoopBackOff` status?
{: #ts-app-pod-crashloop}
{: troubleshoot}
{: support}

**Infrastructure provider**:
* <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
* <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC


Your pods are in a `CrashLoopBackOff` status.
{: tsSymptoms}


When you try to deploy an app that works on community Kubernetes platforms, you might see this status or a related error message because {{site.data.keyword.openshiftshort}} sets up stricter security settings by default than community Kubernetes.
{: tsCauses}


Make sure that you review the [common scenarios where you might need to modify your apps](/docs/openshift?topic=openshift-plan_deploy#openshift_move_apps_scenarios) and follow the docs in the [Moving your apps to OpenShift topic](/docs/openshift?topic=openshift-deploy_app#openshift_move_apps).
{: tsResolve}






