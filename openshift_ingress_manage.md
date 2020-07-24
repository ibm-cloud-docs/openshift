---

copyright:
  years: 2014, 2020
lastupdated: "2020-07-24"

keywords: openshift, roks, rhoks, rhos, nginx, ingress controller

subcollection: openshift

---

{:beta: .beta}
{:codeblock: .codeblock}
{:deprecated: .deprecated}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:gif: data-image-type='gif'}
{:help: data-hd-content-type='help'}
{:important: .important}
{:new_window: target="_blank"}
{:note: .note}
{:pre: .pre}
{:preview: .preview}
{:screen: .screen}
{:shortdesc: .shortdesc}
{:support: data-reuse='support'}
{:table: .aria-labeledby="caption"}
{:tip: .tip}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}



# Managing the Ingress ALB lifecycle
{: #ingress-manage}

Manage the lifecycle of your Ingress application load balancers (ALBs).
{: shortdesc}

<img src="images/icon-version-311.png" alt="Version 3.11 icon" width="30" style="width:30px; border-style: none"/> This information is applicable for clusters that run OpenShift version 3.11 only.
{: important}

Looking to change your ALBs' basic behavior or tune ALB performance? See [Modifying default Ingress settings](/docs/openshift?topic=openshift-ingress-settings).
{: tip}

## Updating ALBs
{: #alb-update}


Manage automatic updates of all Ingress ALB pods in a cluster.
{: shortdesc}

By default, automatic updates to Ingress ALBs are enabled. ALB pods are automatically updated when a new image version is available.

You can disable or enable the automatic updates for all Ingress ALBs in your cluster.
* To disable automatic updates:
  ```
  ibmcloud oc alb autoupdate disable -c <cluster_name_or_ID>
  ```
  {: pre}
* To re-enable automatic updates:
  ```
  ibmcloud oc alb autoupdate enable -c <cluster_name_or_ID>
  ```
  {: pre}

If automatic updates for the Ingress ALB add-on are disabled and you want to update the add-on, you can force a one-time update of your ALB pods by running `ibmcloud oc alb update -c <cluster_name_or_ID>`. When you choose to manually update the add-on, all ALB pods in the cluster are updated to the latest image version. You cannot update an individual ALB or choose which image version to update the add-on to. For example, you cannot change your ALB image to another type when you manually update. Automatic updates remain disabled.

If your ALB pods were recently updated, but a custom configuration for your ALBs is affected by the latest version, you can roll back the update to the version that your ALB pods were previously running. After you roll back an update, automatic updates for ALB pods remain disabled.
```
ibmcloud oc alb rollback --cluster <cluster_name_or_ID>
```
{: pre}


<br />


## Scaling ALBs
{: #scale_albs}

When you create a standard cluster, one public and one private ALB is created in each zone where you have worker nodes. Each ALB can handle 32,768 connections per second. However, if you must process more than 32,768 connections per second, you can scale up your ALBs by increasing the number of ALB pod replicas or by creating more ALBs.
{: shortdesc}

### Increasing the number of ALB pod replicas
{: #alb_replicas}

By default, each ALB has 2 replicas. Scale up your ALB processing capabilities by increasing the number of ALB pods.
{: shortdesc}

1. Get the IDs for your ALBs.
  ```
  ibmcloud oc alb ls -c <cluster_name_or_ID>
  ```
  {: pre}

2. Create a YAML file for an `ibm-ingress-deploy-config` configmap. For each ALB, add `'{"replicas":<number_of_replicas>}'`. Example for increasing the number of ALB pods to 4 replicas:
   ```yaml
   apiVersion: v1
   kind: ConfigMap
   metadata:
     name: ibm-ingress-deploy-config
     namespace: kube-system
   data:
     <alb1-id>: '{"replicas":<number_of_replicas>}'
     <alb2-id>: '{"replicas":<number_of_replicas>}'
     ...
   ```
   {: screen}

3. Create the `ibm-ingress-deploy-config` configmap in your cluster.
  ```
  oc create -f ibm-ingress-deploy-config.yaml
  ```
  {: pre}

4. To pick up the changes, update your ALBs.
  ```
  ibmcloud oc alb update -c <cluster_name_or_ID>
  ```
  {: pre}

5. Verify that the number of ALB pods that are `Ready` are increased to the number of replicas that you specified.
  ```
  oc get pods -n kube-system | grep alb
  ```
  {: pre}

### Creating more ALBs
{: #create_alb}

Scale up your ALB processing capabilities by creating more ALBs.
{: shortdesc}

For example, if you have worker nodes in `dal10`, a default public ALB exists in `dal10`. This default public ALB is deployed as two pods on two worker nodes in that zone. However, to handle more connections per second, you want to increase the number of ALBs in `dal10`. You can create a second public ALB in `dal10`. This ALB is also deployed as two pods on two worker nodes in `dal10`. All public ALBs in your cluster share the same IBM-assigned Ingress subdomain, so the IP address of the new ALB is automatically added to your Ingress subdomain. You do not need to change your Ingress resource files.

You can also use these steps to create more ALBs across zones in your cluster. When you create a multizone cluster, a default public ALB is created in each zone where you have worker nodes. However, default public ALBs are created in only up to three zones. If, for example, you later remove one of these original three zones and add workers in a different zone, a default public ALB is not created in that new zone. You can manually create an ALB to process connections in that new zone.
{: tip}

1. In each zone where you have worker nodes, create an ALB.
  ```
  ibmcloud oc alb create --cluster <cluster_name_or_ID> --type <public_or_private> --zone <zone> --vlan <VLAN_ID> [--user-ip <IP_address>] [--version image_version]
  ```
  {: pre}

  <table>
  <caption>Understanding this command's components</caption>
  <col width="25%">
  <thead>
  <th>Parameter</th>
  <th>Description</th>
  </thead>
  <tbody>
  <tr>
  <td><code>--cluster &lt;cluster_name_or_ID&gt;</code></td>
  <td>The name or ID of the cluster.</td>
  </tr>
  <tr>
  <td><code>--type &lt;public_or_private&gt;</code></td>
  <td>The type of ALB: <code>public</code> or <code>private</code>.</td>
  </tr>
  <tr>
  <td><code>--zone &lt;zone&gt;</code></td>
  <td>The zone where you want to create the ALB.</td>
  </tr>
  <tr>
  <td><code>--vlan &lt;VLAN_ID&gt;</code></td>
  <td>This VLAN must match the ALB public or private <code>type</code> and must be in the same <code>zone</code> as the ALB that you want to create. To see your available VLANs for a zone, run <code>ibmcloud oc worker get --cluster &lt;cluster_name_or_ID&gt; --worker &lt;worker_id&gt;</code> and note the ID for the public or the private VLAN.</td>
  </tr>
  <tr>
  <td><code>--user-ip &lt;IP_address&gt;</code></td>
  <td>Optional: An IP address to assign to the ALB. This IP must be on the <code>vlan</code> that you specified and must be in the same <code>zone</code> as the ALB that you want to create. For more information, see [Viewing available portable public IP addresses](/docs/openshift?topic=openshift-subnets#managing_ips).</td>
  </tr>
  <tr>
  <td><code>--version &lt;image_version&gt;</code></td>
  <td>Optional: The version of the image that you want the ALB to run. To list available versions, run `ibmcloud oc alb versions`.</td>
  </tr>
  </tbody>
  </table>

2. Verify that the ALBs that you created in each zone have a **Status** of `enabled` and that an **ALB IP** is assigned.
  ```
  ibmcloud oc alb ls --cluster <cluster_name_or_ID>
  ```
  {: pre}

  Example output for a cluster in which new public ALBs with IDs of `public-crdf253b6025d64944ab99ed63bb4567b6-alb3` and `public-crdf253b6025d64944ab99ed63bb4567b6-alb4` are created in `dal10` and `dal12`:
  ```
  ALB ID                                            Enabled   Status     Type      ALB IP          Zone    Build                          ALB VLAN ID   NLB Version
  private-crdf253b6025d64944ab99ed63bb4567b6-alb1   false     disabled   private   -               dal12   ingress:411/ingress-auth:315   2294021       -
  private-crdf253b6025d64944ab99ed63bb4567b6-alb2   false     disabled   private   -               dal10   ingress:411/ingress-auth:315   2234947       -
  public-crdf253b6025d64944ab99ed63bb4567b6-alb1    true      enabled    public    169.48.228.78   dal12   ingress:411/ingress-auth:315   2294019       -
  public-crdf253b6025d64944ab99ed63bb4567b6-alb2    true      enabled    public    169.46.17.6     dal10   ingress:411/ingress-auth:315   2234945       -
  public-crdf253b6025d64944ab99ed63bb4567b6-alb3    true      enabled    public    169.49.28.09    dal12   ingress:411/ingress-auth:315   2294019       -
  public-crdf253b6025d64944ab99ed63bb4567b6-alb4    true      enabled    public    169.50.35.62    dal10   ingress:411/ingress-auth:315   2234945       -
  ```
  {: screen}

3. If you later decide to scale down your ALBs, you can disable an ALB. For example, you might want to disable an ALB to use less compute resources on your worker nodes. The ALB is disabled and does not route traffic in your cluster. You can re-enable an ALB at any time by running `ibmcloud oc alb configure classic --alb-id <ALB_ID> --enable`.
  ```
  ibmcloud oc alb configure classic --alb-id <ALB_ID> --disable
  ```
  {: pre}
  </br>

<br />


## Moving ALBs across VLANs
{: #migrate-alb-vlan}

<img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> The information in this topic is specific to classic clusters only.
{: note}

When you [change your worker node VLAN connections](/docs/openshift?topic=openshift-cs_network_cluster#change-vlans), the worker nodes are connected to the new VLAN and assigned new public or private IP addresses. However, ALBs cannot automatically migrate to the new VLAN because they are assigned a stable, portable public or private IP address from a subnet that belongs to the old VLAN. When your worker nodes and ALBs are connected to different VLANs, the ALBs cannot forward incoming network traffic to app pods to your worker nodes. To move your ALBs to a different VLAN, you must create an ALB on the new VLAN and disable the ALB on the old VLAN.
{: shortdesc}

Note that all public ALBs in your cluster share the same IBM-assigned Ingress subdomain. When you create new ALBs, you do not need to change your Ingress resource files.

1. Get the new public or private VLAN that you changed your worker node connections to in each zone.
  1. List the details for a worker in a zone.
    ```
    ibmcloud oc worker get --cluster <cluster_name_or_ID> --worker <worker_id>
    ```
    {: pre}

  2. In the output, note the **ID** for the public or the private VLAN.
    * To create public ALBs, note the public VLAN ID.
    * To create private ALBs, note the private VLAN ID.

  3. Repeat these steps for a worker in each zone so that you have the IDs for the new public or private VLAN in each zone.

2. In each zone, create an ALB on the new VLAN.
  ```
  ibmcloud oc alb create --cluster <cluster_name_or_ID> --type <public_or_private> --zone <zone> --vlan <VLAN_ID> [--user-ip <IP_address>] [--version image_version]
  ```
  {: pre}

  <table>
  <caption>Understanding this command's components</caption>
  <col width="25%">
  <thead>
  <th>Parameter</th>
  <th>Description</th>
  </thead>
  <tbody>
  <tr>
  <td><code>--cluster &lt;cluster_name_or_ID&gt;</code></td>
  <td>The name or ID of the cluster.</td>
  </tr>
  <tr>
  <td><code>--type &lt;public_or_private&gt;</code></td>
  <td>The type of ALB: <code>public</code> or <code>private</code>.</td>
  </tr>
  <tr>
  <td><code>--zone &lt;zone&gt;</code></td>
  <td>The zone where you want to create the ALB.</td>
  </tr>
  <tr>
  <td><code>--vlan &lt;VLAN_ID&gt;</code></td>
  <td>The VLAN ID where you want to create your ALB. This VLAN must match the public or private ALB <code>type</code> and must be in the same <code>zone</code> as the ALB that you want to create.</td>
  </tr>
  <tr>
  <td><code>--user-ip &lt;IP_address&gt;</code></td>
  <td>Optional: An IP address to assign to the ALB. This IP must be on the <code>vlan</code> that you specified and must be in the same <code>zone</code> as the ALB that you want to create. For more information, see [Viewing available portable public IP addresses](/docs/openshift?topic=openshift-subnets#managing_ips).</td>
  </tr>
  <tr>
  <td><code>--version &lt;image_version&gt;</code></td>
  <td>Optional: The version of the image that you want the ALB to run. To list available versions, run `ibmcloud oc alb versions`.</td>
  </tr>
  </tbody>
  </table>

3. Verify that the ALBs that you created on the new VLANs in each zone have a **Status** of `enabled` and that an **ALB IP** address is assigned.
    ```
    ibmcloud oc alb ls --cluster <cluster_name_or_ID>
    ```
    {: pre}

    Example output for a cluster in which new public ALBs are created on VLAN `2294030` in `dal12` and `2234940` in `dal10`:
    ```
    ALB ID                                            Enabled   Status     Type      ALB IP          Zone    Build                          ALB VLAN ID   NLB Version
    private-crdf253b6025d64944ab99ed63bb4567b6-alb1   false     disabled   private   -               dal12   ingress:411/ingress-auth:315   2294021
    private-crdf253b6025d64944ab99ed63bb4567b6-alb2   false     disabled   private   -               dal10   ingress:411/ingress-auth:315   2234947
    public-crdf253b6025d64944ab99ed63bb4567b6-alb1    true      enabled    public    169.48.228.78   dal12   ingress:411/ingress-auth:315   2294019
    public-crdf253b6025d64944ab99ed63bb4567b6-alb2    true      enabled    public    169.46.17.6     dal10   ingress:411/ingress-auth:315   2234945
    public-crdf253b6025d64944ab99ed63bb4567b6-alb3    true      enabled    public    169.49.28.09    dal12   ingress:411/ingress-auth:315   2294030
    public-crdf253b6025d64944ab99ed63bb4567b6-alb4    true      enabled    public    169.50.35.62    dal10   ingress:411/ingress-auth:315   2234940
    ```
    {: screen}

4. Disable each ALB that is connected to the old VLANs.
  ```
  ibmcloud oc alb configure --alb-id <old_ALB_ID> --disable
  ```
  {: pre}

5. Verify that each ALB that is connected to the old VLANs has a **Status** of `disabled`. Only the ALBs that are connected to the new VLANs receive incoming network traffic and communicate with your app pods.
    ```
    ibmcloud oc alb ls --cluster <cluster_name_or_ID>
    ```
    {: pre}

    Example output for a cluster in which the default public ALBs on VLAN `2294019` in `dal12` and `2234945` in `dal10`: are disabled:
    ```
    ALB ID                                            Enabled   Status     Type      ALB IP          Zone    Build
    private-crdf253b6025d64944ab99ed63bb4567b6-alb1   false     disabled   private   -               dal12   ingress:411/ingress-auth:315   2294021
    private-crdf253b6025d64944ab99ed63bb4567b6-alb2   false     disabled   private   -               dal10   ingress:411/ingress-auth:315   2234947
    public-crdf253b6025d64944ab99ed63bb4567b6-alb1    false     disabled   public    169.48.228.78   dal12   ingress:411/ingress-auth:315   2294019
    public-crdf253b6025d64944ab99ed63bb4567b6-alb2    false     disabled   public    169.46.17.6     dal10   ingress:411/ingress-auth:315   2234945
    public-crdf253b6025d64944ab99ed63bb4567b6-alb3    true      enabled    public    169.49.28.09    dal12   ingress:411/ingress-auth:315   2294030
    public-crdf253b6025d64944ab99ed63bb4567b6-alb4    true      enabled    public    169.50.35.62    dal10   ingress:411/ingress-auth:315   2234940
    ```
    {: screen}

6. Optional for public ALBs: Verify that the IP addresses of the new ALBs are listed under the IBM-provided Ingress subdomain for your cluster. You can find this subdomain by running `ibmcloud oc cluster get --cluster <cluster_name_or_ID>`.
  ```
  nslookup <Ingress_subdomain>
  ```
  {: pre}

  Example output:
  ```
  Non-authoritative answer:
  Name:    mycluster-<hash>-0000.us-south.containers.appdomain.cloud
  Addresses:  169.49.28.09
            169.50.35.62
  ```
  {: screen}

7. Optional: If you no longer need the subnets on the old VLANs, you can [remove them](/docs/openshift?topic=openshift-subnets#remove-subnets).

<br />


## Increasing the restart readiness check time for ALB pods
{: #readiness-check}

Increase the amount of time that ALB pods have to parse large Ingress resource files when the ALB pods restart.
{: shortdesc}

When an ALB pod restarts, such as after an update is applied, a readiness check prevents the ALB pod from attempting to route traffic requests until all of the Ingress resource files are parsed. This readiness check prevents request loss when ALB pods restart. By default, the readiness check waits 15 seconds after the pod restarts to start checking whether all Ingress files are parsed. If all files are parsed 15 seconds after the pod restarts, the ALB pod begins to route traffic requests again. If all files are not parsed 15 seconds after the pod restarts, the pod does not route traffic, and the readiness check continues to check every 15 seconds for a maximum timeout of 5 minutes. After 5 minutes, the ALB pod begins to route traffic.

If you have very large Ingress resource files, it might take longer than 5 minutes for all of the files to be parsed. You can change the default values for the readiness check interval rate and for the total maximum readiness check timeout by adding the `ingress-resource-creation-rate` and `ingress-resource-timeout` settings to the `ibm-cloud-provider-ingress-cm` configmap.

1. Edit the configuration file for the `ibm-cloud-provider-ingress-cm` configmap resource.
    ```
    oc edit cm ibm-cloud-provider-ingress-cm -n kube-system
    ```
    {: pre}

2. In the **data** section, add the `ingress-resource-creation-rate` and `ingress-resource-timeout` settings. Values can be formatted as seconds (`s`) and minutes (`m`). Example:
   ```yaml
   apiVersion: v1
   data:
     ingress-resource-creation-rate: 1m
     ingress-resource-timeout: 6m
     keep-alive: 8s
     private-ports: 80;443
     public-ports: 80;443
   ```
   {: codeblock}

3. Save the configuration file.

4. Verify that the configmap changes were applied. The changes are applied to your ALBs automatically.
   ```
   oc get cm ibm-cloud-provider-ingress-cm -n kube-system -o yaml
   ```
   {: pre}


