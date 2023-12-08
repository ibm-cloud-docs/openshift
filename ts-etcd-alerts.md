---

copyright:
  years: 2023, 2023
lastupdated: "2023-12-08"

keywords: etcd, help, alert

subcollection: containers, openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why am I receiving multiple etcd alerts?
{: #ts-addon-etcd-alerts}
{: support}

You receive multiple alerts for `etcdHighNumberOfLeaderChanges` or `etcdExcessiveDatabaseGrowth`, with descriptions similar to the following messages.
{: tsSymptoms}

```txt
"etcd": 7.5 leader changes within the last 15 minutes. Frequent elections may be a sign of insufficient resources, high network latency, or disruptions by other components and should be investigated.
```
{: screen}

```txt
"etcd cluster "etcd": Observed surge in etcd writes leading to 50% increase in database size over the past four hours on etcd instance, please check as it might be disruptive.
```
{: screen}

The cluster etcd database is located on the cluster control plane, which is maintained by IBM. Metrics from three separate etcd instances are pushed to a single pod in the cluster, but the source of the metrics is not always distinguished. When these metrics are collected by Prometheus they might be read as originating from a single etcd instance rather than multiple separate instances, resulting in a false alert for high rates of activity. In this case, there is no underlying issue and the alerts are triggered falsely. 
{: tsCauses}

Often, the `etcdHighNumberOfLeaderChanges` and `etcdExcessiveDatabaseGrowth` do not indicate an underlying issue and can be ignored. If you want to validate that the alerts are false, you can contact customer support. Open a [support case](/docs/get-support?topic=get-support-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.
{: tsResolve}

