---

copyright:
  years: 2026, 2026
lastupdated: "2026-10-29"

keywords: openshift, classic, vpc, migrate, cut over, cutover, validate, decommission, dns, traffic

subcollection: openshift

content-type: howto

---

{{site.data.keyword.attribute-definition-list}}

# Cut over and validate
{: #vpc-migrate-cutover}

[Classic infrastructure]{: tag-classic-inf}

Redirect live traffic to the VPC cluster, validate that all workloads are functioning correctly, and complete the migration wizard.
{: shortdesc}

## Before you begin
{: #vpc-migrate-cutover-prereqs}

- All workloads are running on the VPC cluster and verified. See [Migrate workloads](/docs/openshift?topic=openshift-vpc-migrate-workloads).
- External DNS TTLs for your application hostnames have been lowered to 60–300 seconds before the cutover window, so propagation completes quickly.
- You have a rollback plan: the Classic cluster is still running and can receive traffic if cutover validation fails.
- [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

## Step 1: Perform a final data sync
{: #vpc-migrate-cutover-sync}

Before redirecting traffic, quiesce writes on the Classic cluster and copy any incremental data changes to the VPC cluster. This minimizes data divergence during the cutover window. Plan a maintenance window for this step — duration depends on your data volume. During this window, stateful applications on the Classic cluster will be temporarily unavailable.

### From the console
{: #vpc-migrate-cutover-sync-ui}
{: ui}

For each stateful application:

1. From the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/containers/cluster-management/clusters){: external}, click your Classic cluster.
2. Click **Kubernetes dashboard** to open the cluster console.
3. Navigate to **Workloads** > **Deployments** and click the deployment you want to quiesce.
4. Click **Edit** and set the **Replicas** field to `0`, then click **Update** to stop writes.
5. Copy any data changed since the initial workload migration to the VPC PVCs.
6. On your VPC cluster, navigate to the same deployment and restore the replica count to its original value to confirm data integrity.

### From the CLI
{: #vpc-migrate-cutover-sync-cli}
{: cli}

For each stateful application:

1. Scale down the Classic deployment to zero replicas to stop writes. Replace `DEPLOYMENT_NAME` and `NAMESPACE` with your deployment details.

   ```sh
   oc scale deployment DEPLOYMENT_NAME --replicas=0 -n NAMESPACE
   ```
   {: pre}

   Example output:
   ```text
   deployment.apps/DEPLOYMENT_NAME scaled
   ```
   {: screen}

2. Copy any data changed since the initial workload migration to the VPC PVCs.

3. Scale up the VPC deployment to confirm data integrity. Replace `ORIGINAL_REPLICA_COUNT` with the number of replicas the deployment had before you scaled it down.

   ```sh
   oc scale deployment DEPLOYMENT_NAME --replicas=ORIGINAL_REPLICA_COUNT -n NAMESPACE
   ```
   {: pre}

   Example output:
   ```text
   deployment.apps/DEPLOYMENT_NAME scaled
   ```
   {: screen}

### From the API
{: #vpc-migrate-cutover-sync-api}
{: api}

For each stateful application, patch the deployment replica count using the Kubernetes API on your Classic cluster.

1. Scale down the Classic deployment to stop writes. Replace `NAMESPACE`, `DEPLOYMENT_NAME`, and the cluster API server address as appropriate.

   ```sh
   curl -X PATCH \
     "https://CLASSIC_KUBE_API_SERVER/apis/apps/v1/namespaces/NAMESPACE/deployments/DEPLOYMENT_NAME" \
     -H "Authorization: Bearer KUBE_TOKEN" \
     -H "Content-Type: application/merge-patch+json" \
     -d '{"spec":{"replicas":0}}'
   ```
   {: pre}

   The Kubernetes API returns the full patched deployment object. Confirm `spec.replicas` is `0` in the response:
   ```json
   {
     "apiVersion": "apps/v1",
     "kind": "Deployment",
     "metadata": { "name": "DEPLOYMENT_NAME", "namespace": "NAMESPACE" },
     "spec": { "replicas": 0 }
   }
   ```
   {: screen}

2. Copy any data changed since the initial workload migration to the VPC PVCs.

3. Scale up the VPC deployment to confirm data integrity. Replace `ORIGINAL_REPLICA_COUNT` with the original number of replicas.

   ```sh
   curl -X PATCH \
     "https://VPC_KUBE_API_SERVER/apis/apps/v1/namespaces/NAMESPACE/deployments/DEPLOYMENT_NAME" \
     -H "Authorization: Bearer KUBE_TOKEN" \
     -H "Content-Type: application/merge-patch+json" \
     -d '{"spec":{"replicas":ORIGINAL_REPLICA_COUNT}}'
   ```
   {: pre}

   Confirm `spec.replicas` is restored in the response:
   ```json
   {
     "apiVersion": "apps/v1",
     "kind": "Deployment",
     "metadata": { "name": "DEPLOYMENT_NAME", "namespace": "NAMESPACE" },
     "spec": { "replicas": 3 }
   }
   ```
   {: screen}

## Step 2: Get the VPC cluster Ingress ALB addresses
{: #vpc-migrate-cutover-alb}

Before you update DNS, retrieve the VPC cluster's ALB IP addresses. Note the **ALB IP** or **hostname** values for the public ALBs — you need these to update your DNS records to point to the VPC cluster.

### From the console
{: #vpc-migrate-cutover-alb-ui}
{: ui}

1. From the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/containers/cluster-management/clusters){: external}, click your VPC cluster.
2. Click **Networking** > **Ingress** in the left navigation menu.
3. Note the **Ingress subdomain** and the **ALB IP addresses** listed for the public ALBs.

### From the CLI
{: #vpc-migrate-cutover-alb-cli}
{: cli}

1. List the ALBs on the VPC cluster. Note the **ALB IP** or **Hostname** values in the `public` rows.

   ```sh
   ibmcloud oc ingress alb ls --cluster VPC_CLUSTER_NAME
   ```
   {: pre}

   Example output:
   ```text
   ALB ID                                            Status    Type      ALB IP          Zone         Build
   private-cra1b2c3d4-alb1                           enabled   private   10.240.0.6      us-south-1   ingress:/2458
   public-cra1b2c3d4-alb1                            enabled   public    169.46.45.100   us-south-1   ingress:/2458
   public-cra1b2c3d4-alb2                            enabled   public    169.46.109.200  us-south-2   ingress:/2458
   public-cra1b2c3d4-alb3                            enabled   public    169.48.200.150  us-south-3   ingress:/2458
   ```
   {: screen}

### From the API
{: #vpc-migrate-cutover-alb-api}
{: api}

1. Retrieve the public ALB IP addresses for the VPC cluster.

   ```sh
   curl -X GET "https://REGION.containers.cloud.ibm.com/v1/albs?cluster=VPC_CLUSTER_ID" \
     -H "Authorization: Bearer $(ibmcloud iam oauth-tokens --output json | jq -r '.iam_token')"
   ```
   {: pre}

   Example response (truncated to public ALBs):
   ```json
   [
     { "albID": "public-cra1b2c3d4-alb1", "albType": "public", "enable": true, "albIP": "169.46.45.100",   "zone": "us-south-1" },
     { "albID": "public-cra1b2c3d4-alb2", "albType": "public", "enable": true, "albIP": "169.46.109.200",  "zone": "us-south-2" },
     { "albID": "public-cra1b2c3d4-alb3", "albType": "public", "enable": true, "albIP": "169.48.200.150",  "zone": "us-south-3" }
   ]
   ```
   {: screen}

   Note the `albIP` values for the public ALBs. You need them in step 3.

## Step 3: Redirect DNS
{: #vpc-migrate-cutover-dns}

DNS record updates are performed in your external DNS provider's interface or API. The specific steps vary by provider.
{: note}

Update your external DNS provider to point application hostnames to the VPC cluster's ALB IP addresses or hostname. The migration plan generated in the [Migrate step](/docs/openshift?topic=openshift-vpc-migrate-workloads) lists the Classic-to-VPC Ingress host mappings.

Because you lowered DNS TTLs 24–48 hours before cutover, propagation completes within the TTL window (60–300 seconds).

### Transfer custom domains
{: #vpc-migrate-cutover-dns-domains}
{: ui}

For applications using IBM-managed Ingress subdomains with a custom domain, deregister the custom domain from the Classic cluster and register it with the VPC cluster. The migration wizard links to this guidance from the **Cutover** step.

1. In the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/containers/cluster-management/clusters){: external}, click your Classic cluster.
2. In the left navigation, click **Ingress** > **Domains**. Locate the custom domain and click **Deregister** to remove it from the Classic cluster.
3. From the **Clusters** page in the console, click your VPC cluster.
4. In the left navigation, click **Ingress** > **Domains**. Register the same custom domain with the VPC cluster.

## Step 4: Validate workloads
{: #vpc-migrate-cutover-validate}

After DNS has propagated, validate each application from outside the cluster.

### From the console
{: #vpc-migrate-cutover-validate-ui}
{: ui}

1. From the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/containers/cluster-management/clusters){: external}, click your VPC cluster.
2. Check the **Node status**, **Control plane status**, and **Ingress status** tiles. All should show **Healthy**.
3. Click **Kubernetes dashboard** to navigate to **Workloads** > **Pods**. Filter by each migrated namespace and confirm all pods show **Running** or **Completed**.
4. Test each application endpoint from a browser or external tool to confirm HTTP responses are correct.
5. If any application is not working as expected, roll back by updating your DNS records to point back to the Classic cluster ALB addresses and investigate the issue before retrying.

### From the CLI
{: #vpc-migrate-cutover-validate-cli}
{: cli}

1. Confirm all pods remain `Running` or `Completed` across all namespaces:

   ```sh
   oc get pods --all-namespaces
   ```
   {: pre}

   Example output:
   ```text
   NAMESPACE    NAME                          READY   STATUS    RESTARTS   AGE
   production   my-app-6d4b9f7d8-xk2np        1/1     Running   0          12m
   production   my-db-0                        1/1     Running   0          12m
   monitoring   prometheus-5c8d9b7f4-lm3qr     1/1     Running   0          11m
   staging      my-app-7f5c8b9d6-pn4rs         1/1     Running   0          10m
   ```
   {: screen}

   Investigate any pod that shows `Error`, `CrashLoopBackOff`, or `Pending`.

2. Test each application endpoint. Confirm HTTP status codes and response content are correct.

3. Check application logs for errors in each migrated namespace. Look for stack traces, connection errors, or repeated restarts.

   ```sh
   oc logs -n NAMESPACE DEPLOYMENT_NAME --tail=100
   ```
   {: pre}

4. Review cluster events for warnings across all namespaces:

   ```sh
   oc get events --all-namespaces --sort-by='.lastTimestamp' | tail -30
   ```
   {: pre}

   Example output:
   ```text
   NAMESPACE    LAST SEEN   TYPE      REASON              OBJECT                          MESSAGE
   production   2m          Normal    Pulled              pod/my-app-6d4b9f7d8-xk2np      Container image already present on machine
   production   2m          Normal    Started             pod/my-app-6d4b9f7d8-xk2np      Started container my-app
   monitoring   3m          Normal    ScalingReplicaSet   replicaset/prometheus-5c8d9b7f4  Scaled up replica set
   ```
   {: screen}

5. If any application is not working as expected, roll back by updating the DNS records to point back to the Classic cluster ALB addresses and investigate the issue before retrying.

### From the API
{: #vpc-migrate-cutover-validate-api}
{: api}

1. Confirm the VPC cluster is healthy:

   ```sh
   curl -X GET "https://REGION.containers.cloud.ibm.com/v1/clusters/VPC_CLUSTER_ID" \
     -H "Authorization: Bearer $(ibmcloud iam oauth-tokens --output json | jq -r '.iam_token')" \
     | jq '{state: .state, status: .status, masterStatus: .masterStatus, ingressStatus: .ingressHostname}'
   ```
   {: pre}

   Expected output:
   ```json
   {
     "state": "normal",
     "status": "All Workers Normal",
     "masterStatus": "Ready",
     "ingressStatus": "healthy"
   }
   ```
   {: screen}

2. Confirm all pods are running on the VPC cluster:

   ```sh
   oc get pods --all-namespaces --output json | jq '[.items[] | select(.status.phase != "Running" and .status.phase != "Succeeded") | {namespace: .metadata.namespace, name: .metadata.name, phase: .status.phase}]'
   ```
   {: pre}

   An empty array `[]` confirms all pods are in a running or completed state. Investigate any pods listed.

3. If any application is not working as expected, roll back by updating your DNS records to point back to the Classic cluster ALB addresses and investigate the issue before retrying.

## Step 5: Stabilization period
{: #vpc-migrate-cutover-stabilize}

Keep the Classic cluster running but idle for a stabilization period of at least [VERIFY: confirm recommended stabilization duration with engineering] hours. Do not delete the Classic cluster until you are confident that:

- All traffic is flowing through the VPC cluster
- Application metrics, error rates, and performance are normal
- No users or systems are still directing requests to the Classic cluster

### From the console
{: #vpc-migrate-cutover-stabilize-ui}
{: ui}

During the stabilization period, monitor the VPC cluster health from the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/containers/cluster-management/clusters){: external}:

- Review the **Node status**, **Add-on status**, and **Ingress status** tiles on the cluster overview page.
- Watch for any alerts in the cluster event log.
- Confirm the Classic cluster overview page shows no active traffic by checking that no new events appear under **Kubernetes dashboard** for that cluster.

### From the CLI
{: #vpc-migrate-cutover-stabilize-cli}
{: cli}

During the stabilization period, run the following checks periodically:

1. Confirm all worker nodes on the VPC cluster remain in `normal` state:

   ```sh
   ibmcloud oc workers --cluster VPC_CLUSTER_NAME
   ```
   {: pre}

   Example output:
   ```text
   ID                                                     Public IP        Private IP      Flavor      State    Status   Zone
   kube-a1b2c3d4-vpc01worker-default-000001f1             169.46.45.101    10.240.0.11     bx2.4x16    normal   Ready    us-south-1
   kube-a1b2c3d4-vpc01worker-default-00000216             169.46.109.102   10.240.64.12    bx2.4x16    normal   Ready    us-south-2
   kube-a1b2c3d4-vpc01worker-default-000003ab             169.48.200.103   10.240.128.13   bx2.4x16    normal   Ready    us-south-3
   ```
   {: screen}

2. Check for any DNS caching in client systems that might still resolve to Classic ALB addresses by querying the Classic cluster's subdomain and confirming it is no longer receiving traffic.

### From the API
{: #vpc-migrate-cutover-stabilize-api}
{: api}

During the stabilization period, poll the VPC cluster state periodically to confirm it remains healthy:

```sh
curl -X GET "https://REGION.containers.cloud.ibm.com/v1/clusters/VPC_CLUSTER_ID" \
  -H "Authorization: Bearer $(ibmcloud iam oauth-tokens --output json | jq -r '.iam_token')" \
  | jq '{state: .state, workerCount: .workerCount, masterStatus: .masterStatus}'
```
{: pre}

Expected output:
```json
{
  "state": "normal",
  "workerCount": 3,
  "masterStatus": "Ready"
}
```
{: screen}

## Step 6: Restore DNS TTLs
{: #vpc-migrate-cutover-ttl}

After the stabilization period, restore DNS TTLs to their original values (typically 300–3600 seconds). Update these settings in your external DNS provider's interface or API.

## Step 7: Finish migration
{: #vpc-migrate-cutover-finish}

The **Finish migration** button is active only after all checklist items are selected. After you confirm, the migration wizard closes and you return to the eligible clusters list. Your Classic cluster continues to run until you delete it separately.
{: note}

When you are ready to close out the migration, click **Finish migration** in the wizard. A confirmation modal titled **Cutover and finish migration** appears. Verify each item in the checklist before confirming:

- Completed the final data sync
- Deregistered the domain from the Classic cluster and registered it with the VPC cluster
- Validated all workloads on the VPC cluster
- Kept the Classic cluster running for the recommended stabilization period [VERIFY: confirm recommended duration with engineering]
- Restored DNS TTLs to their original values
- Using `nslookup`, confirmed the domain points to the VPC ALB or NLB and all features work

## Next steps
{: #vpc-migrate-cutover-next}

The migration wizard is complete. To finish removing your Classic infrastructure, [delete the Classic cluster](/docs/openshift?topic=openshift-vpc-migrate-decommission).
