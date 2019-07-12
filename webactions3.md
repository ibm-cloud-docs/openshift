---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-12"

keywords: web actions, serverless, functions

subcollection: cloud-functions

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:gif: data-image-type='gif'}



# Creating web actions
{: #actions_web}

When you create a web action, the result is a URL that can be used to trigger the action from any web app for testing.
{: shortdesc}




## Why use web actions instead of standard actions?

### 1. Run web actions anonymously

Web action activations are associated with the user that created the action, rather than the caller of the action. Usually, for API calls to apps like Github, you would include a username and token with the API call for either a specific user or a functional ID. When you use a web action, those kinds of credentials are not required. A web action is accessible through a REST interface without the need for credentials.
{: important}

Though you are not required to use credentials with web actions, you can implement your own authentication and authorization, or OAuth flow. To configure a web action with credentials, see [Securing web actions](#actions_web_secure).

