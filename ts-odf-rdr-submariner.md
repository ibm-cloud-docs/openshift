---

copyright:
  years: 2026
lastupdated: "2026-07-23"

keywords: openshift data foundation, ODF, disaster recovery, submariner, gateway, connectivity, ODF-DR, regional disaster recovery, RDR

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why is Submariner connectivity lost or gateway labels missing after an upgrade?
{: #ts-odf-rdr-submariner}
{: troubleshoot}
{: support}

[Virtual Private Cloud]{: tag-vpc}
[4.21 and later]{: tag-red}

After upgrading your ODF Regional Disaster Recovery (RDR) environment, Submariner connectivity between clusters is lost or worker nodes are missing their gateway labels.
{: tsSymptoms}

Worker node upgrades can remove node labels, including the Submariner gateway labels that are required for inter-cluster connectivity. When gateway labels are removed, Submariner cannot route traffic between clusters, which disrupts ODF-DR replication and failover.
{: tsCauses}

Reapply the Submariner gateway labels and verify that connectivity is restored.
{: tsResolve}

1. Identify which worker nodes are missing the gateway label.

   ```sh
   oc get nodes --show-labels | grep submariner
   ```
   {: pre}

2. Reapply the gateway label to the affected worker nodes. Replace `<node_name>` with the name of each affected node.

   ```sh
   oc label node <node_name> submariner.io/gateway=true
   ```
   {: pre}

3. If needed, adjust the gateway replica count from the ACM console.
   1. In the ACM console, go to **Infrastructure** > **Clusters** > **Cluster sets** and select your cluster set.
   2. Go to the **Submariner add-ons** tab.
   3. Select the affected cluster and adjust the gateway count.

4. Verify that Submariner gateway pods become healthy.

   ```sh
   oc get pods -n submariner-operator
   ```
   {: pre}

5. Verify that inter-cluster connectivity is restored.
   1. In the ACM console, go to **Infrastructure** > **Clusters** > **Cluster sets** and select your cluster set.
   2. Go to the **Submariner add-ons** tab and confirm that connectivity shows as healthy for all clusters.

For more information, see [Workaround for Submariner connectivity issues](https://access.redhat.com/solutions/7144422){: external} in the Red Hat documentation.
