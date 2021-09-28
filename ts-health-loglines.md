---

copyright: 
  years: 2014, 2021
lastupdated: "2021-09-28"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift
content-type: troubleshoot

---




{{site.data.keyword.attribute-definition-list}}


# Why are my log lines so long?
{: #long_lines}

**Infrastructure provider**:
* <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
* <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC


You set up a logging configuration in your cluster to forward logs to an external syslog server. When you view logs, you see a long log message. Additionally, in Kibana, you might be able to see only the last 600 - 700 characters of the log message.
{: tsSymptoms}


A long log message might be truncated due to its length before it is collected by Fluentd, so the log might not be parsed correctly by Fluentd before it is forwarded to your syslog server.
{: tsCauses}


To limit line length, you can configure your own logger to have a maximum length for the `stack_trace` in each log.
{: tsResolve}

For example, if you are using Log4j for your logger, you can use an [`EnhancedPatternLayout`](http://logging.apache.org/log4j/1.2/apidocs/org/apache/log4j/EnhancedPatternLayout.html){: external} to limit the `stack_trace` to 15KB.




