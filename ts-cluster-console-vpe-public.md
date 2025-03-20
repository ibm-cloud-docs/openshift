---

copyright:
  years: 2025, 2025
lastupdated: "2025-03-20"


keywords: openshift, console, web, connect, public

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# VPC clusters with a public and private service endpoint: Why can't I connect to the OpenShift console?
{: #ts-cluster-console-vpe-public}

Troubleshoot problems connecting to the OpenShift console on a cluster that has both a public and private service endpoint.

The information in this trouble shooting guide pertains to VPC clusters with both a public and a private service endpoint. 
{: important}

## 1. Understanding the cluster connection flow
{: #ts-console-vpe-public-flow}



The following diagram shows the connection flow for a VPC cluster with both pubic and private service endpoints to connect to the OpenShift web console. Note that all connections from the web browser to the cluster components happen over the public network. Review this diagram and the following descriptions to better understand what troubleshooting steps might be required. 

![OpenShift web console connection flow for a VPC cluster with both public and private service endpoints](images/VPC-ROKS-Public-Private-Openshift-Console.svg){: caption="OpenShift web console connection flow for a VPC cluster with both public and private service endpoints."}

1. The web browser connects to the cluster master API server. A signed certificate is exchanged and a redirect instructs the web browser to instead connect to the OpenShift console public load balancer. 
2. (a) The web browser connects to the OpenShift console load balancer that exposes the OpenShift console. (b) This request is sent to one of the two openshift-console pods. 
3. The openshift-console pod connects via the public network to the cluster master OAuth server port to check if the connection is already authenticated. If the request is already authenticated, the connection to the OpenShift web console is complete and the web console can be accessed. If the request is not authenticated, the user is redirected to the cluster OAuth service on the cluster master. 
4. The web browser connects to the cluster's OAuth server port, which redirects the client to IAM. 
5. The web browser connects to IAM over the public network. The user enters their password and, if required, a 2FA verification. If this step is successful, the user is redirected back to the cluster's OAuth server. 
6. The web browser connects to the cluster's OAuth server port again. The connection is redirected back to the OpenShift console load balancer. 
7. The web browser connects to the OpenShift console load balancer, which exposes the OpenShift console. This request is sent to one of the two openshift-console pods, which again connect to the cluster master OAuth server port to check of the connection is already authenticated. If the user has entered their password and 2FA verification,  the authentication is validated and the user is connected to the OpenShift console main web page.


## 2. Check your VPC and cluster configuration
{: #ts-console-vpe-public-config}

1. Ensure that your web browser has access to the public network so it can connect to the cluster apiserver, the OpenShift console load balancer, and IAM (which use both `iam.cloud.ibm.com` and `login.ibm.com`)
2. Ensure that if you have modified any security groups, ACLs, or Context-Base Restriction (CBR) rules for this cluster or load balancer, that they allow traffic from this web browser to the those resources


## 3. Gather cluster data
{: #ts-console-vpe-public-data}

Follow these steps to gather the cluster information needed for troubleshooting. The outputs you gather with these commands are used in later steps. 

1. Find the cluster API server URL. In later commands, this URL is referred to as `${CLUSTER_APISERVER_URL}`.
    1. Run the `ibmcloud ks cluster get -c <cluster-id>` command. 
        ```sh
        ibmcloud oc cluster get -c <cluster-id>
        ```
        {: pre}
        
    2. In the `Master` section of the output, find the `URL`. The URL should be in the following format: `https://c<XXX>-e.<REGION>.containers.cloud.ibm.com:<YYYYY>`.


2. Find the cluster OAuth URL. In later commands, this URL is referred to as `${CLUSTER_OAUTH_URL}`.
    1. Run the `kubectl get --raw /.well-known/oauth-authorization-server | grep issuer` command. Do not use the `ibmcloud oc cluster get -c <CLUSTER-ID>`, as this command might return a different URL. 
        ```sh
        kubectl get --raw /.well-known/oauth-authorization-server | grep issuer
        ```
        {: pre}

    2. The URL should be in the following format: `https://c<XXX>-e.<REGION>.containers.cloud.ibm.com:<ZZZZZ>`.

3. Find the Ingress subdomain. In later commands, this subdomain is referred to as `${CONSOLE_LOAD_BALANCER}`.
    1. Run the `ibmcloud oc cluster get -c <CLUSTER-ID>` command.
        ```sh
        ibmcloud oc cluster get -c <CLUSTER-ID>
        ```
        {: pre}

    2. In the output, find the subdomain that matches the following format: `<CLUSTER-NAME-PLUS-RANDOM-UNIQUE-STRING>.<REGION>.containers.appdomain.cloud`. Note that if you have configured a custom Ingress subdomain, the format will instead match your custom configuration. 

## 4. Verify connections and troubleshoot
{: #ts-console-vpe-public-verify}

Follow these steps to check the connections described in the [connection flow](#ts-console-vpe-public-flow). If you find a problem with a connection, use the information to troubleshoot the issue.

1. Verify that Ingress is healthy and that the router and console pods are healthy. 
    1. Run the commands.
        ```sh
        ibmcloud oc cluster get -c <CLUSTERID>
        ibmcloud oc ingress status-report get -c <CLUSTERID>
        ```
        {: pre}

    2. If the output shows an error status, use the [Ingress troubleshooting documentation](/docs/openshift?topic=openshift-ingress-status) to resolve the issue. 

2. Verify that the OpenShift cluster operators are healthy.
    1. Run the command.
        ```sh
        oc get clusteroperators
        ```
        {: pre}

    2. If the output shows that any operators are not healthy or are not running at the current version, use the [OpenShift cluster version troubleshooting documentation](https://cloud.ibm.com/docs/openshift?topic=openshift-ts-cluster-version-downlevel) to resolve the issue. Or, you can search the IBM and Red Hat documentation for any specific errors that are shown. 
    3. If the console operator specifically is not healthy, check the `openshift-console/console...` and `openshift-console-operator/console-operator...` pod logs to see if a security group, ACL or DNS customization is preventing the pods from connecting to either the OAuth port or the OpenShift console URL. A security group, ACL or DNS might be configured in a way that prevents the connection. 

3. Verify that the connection to the cluster master API server is successful. 
    1. Run the command. Specify the cluster apiserver URL you found in [previous steps](#ts-console-vpe-public-data).
        ```sh
        curl -k -vvv ${CLUSTER_APISERVER_URL}/version
        ```
        {: pre}

    2. If the connection is not successful, make the following checks and resolve any issues you find. 
        1. Check that the cluster master is healthy by running the `ibmcloud oc cluster get -c <CLUSTER-ID>` command. See [Reviewing master health](/docs/openshift?topic=openshift-debug_master) for information on resolving cluster master issues. 
        2. Check that the hostname portion of the URL is resolved via DNS. Use the `dig $(echo ${CLUSTER_APISERVER_URL} | cut -d/ -f3 | cut -d: -f1)` command and specify the cluster API server URL. 
        3. Check if any Context Based Restriction (CBR) rules on the cluster prevent the client from connecting to the cluster API server. You can test this by temporarily adding a network zone to your public CBR rule that allows all IPs and subnets. If this temporary change resolves the issue, make the necessary changes to the rule to allow the traffic.

4. Verify that the connection to the cluster load balancer exposing the OpenShift console is successful. 
    1. Run the command. Specify the Ingress subdomain you found in the [previous steps](#ts-console-vpe-public-data).
        ```sh
        curl -k -vvv https://console-openshift-console.${CONSOLE_LOAD_BALANCER}/
        ```
        {: pre}

    2. If the connection is not successful, make the following checks and resolve any issues you find. 
        1. Check that the hostname portion of the subdomain is resolved via DNS. Use the `dig console-openshift-console.${CONSOLE_LOAD_BALANCER}` command. 
        2. If you have modified any security groups, ACLs, or custom VPC routes that are applied to the load balancer, check if any changes or rules you applied prevent the connection. If you have not modified any of these components and they use the default values, you can skip this step.
        
5. Verify that the connection to the cluster OAuth server is successful. 
    1. Run the command. Specify the cluster OAuth URL you found in the [previous steps](#ts-console-vpe-public-data).
        ```sh
        curl -k -vvv ${CLUSTER_OAUTH_URL}/healthz
        ```
        {: pre}

    2. If the connection is not successful, make the following checks and resolve any issues you find. 
        1. Check that your cluster master is healthy by running the `ibmcloud oc cluster get -c <CLUSTER-ID>` command. See [Reviewing master health](/docs/openshift?topic=openshift-debug_master) for information on resolving cluster master issues. 
        2. Check that the hostname portion of the cluster OAuth URL is resolved via DNS. Use the `dig $(echo ${CLUSTER_OAUTH_URL} | cut -d/ -f3 | cut -d: -f1)` and specify the cluster OAuth URL. 
        3. Check if any Context Based Restriction (CBR) rules on the cluster prevent the client from connecting to the cluster OAuth server. You can test this by temporarily adding a network zone to your public CBR rule that allows all IPs and subnets. If this temporary change resolves the issue, make the necessary changes to the rule to allow the traffic.

6. Verify that the connection to IAM is successful. 
    1. Run the commands.
        ```sh
        curl -vvv https://iam.cloud.ibm.com/healthz
        curl -vvv -o /dev/null -s https://login.ibm.com/
        ```
        {: pre}

    2. If either of these commands fail, check that the client system is able to connect the these URLs reliably and that the URLs are not blocked by any client or corporate firewalls. Note that these URLs require access to the public internet. 

## 5. Contact support
{: #ts-console-vpe-public-support}

If you completed all the above steps and have not resolved the issue, contact support. Open a [support case](/docs/account?topic=account-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.. 



