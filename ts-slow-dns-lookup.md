---

copyright: 
  years: 2023, 2023
lastupdated: "2023-05-26"

keywords: openshift, dns

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}





# Why are DNS lookups from certain pods so slow?
{: #ts-slow-dns-lookup}
{: support}

Certain containers that are based on Alpine Linux, such as NGINX, have issues with DNS query handling that can cause them to not process valid DNS responses. A small percentage of DNS lookups from these pods can take over 5 seconds instead of the typical <80ms. If the timeout that is set for your application is less than 5 seconds, the DNS lookups can time out.
{: tsSymptoms}

To test whether your pod has this problem, log in to it and verify that curl is installed. You can install curl with the `apk add curl` command. Then, inside the pod run the following command.

```sh
for i in $(seq 1 50); do curl -k -w "time_namelookup: %{time_namelookup}\n" -so /dev/null "https://www.ibm.com/"; done
```
{: pre}

This issue might be caused by the way DNS responses are handled in these pods. For example, when an IPv6 (AAAA record) and an IPv4 (A record) response are returned at nearly the same time, one of the two responses might not be processed, causing the DNS client to not register the response. After a 5 second delay, the DNS client sends out a new request.
{: tsCauses}

You can resolve this issue in one of the following ways.
{: tsResolve}

- (Preferred) Use a base image for your container that does not have this problem, such as Alpine 3.18. You can also replace Alpine with [ubi-minimal](https://hub.docker.com/r/redhat/ubi8-minimal){: external}.
- Add `options single-request-reopen` or `options single-request` options to the client pod's `/etc/resolv.conf` file. For example, use the following `postStart` command to add these options to your pod. These options tell the DNS client to send out only one request (A or AAAA) at a time, and avoids the problem where two responses come back at nearly the same time.

```yaml
  lifecycle:
  postStart:
    exec:
      command:
      - /bin/sh
      - -c 
      - "/bin/echo 'options single-request-reopen' >> /etc/resolv.conf"

```
{: codeblock}
  



