---

copyright:
  years: 2017, 2021
lastupdated: "2021-03-22"

keywords: Centralized security, security management, alerts, security risk, insights, threat detection

subcollection: security-advisor

---

{:codeblock: .codeblock}
{:screen: .screen}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:gif: data-image-type='gif'}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:tip: .tip}
{:preview: .preview}
{:deprecated: .deprecated}
{:beta: .beta}
{:term: .term}
{:shortdesc: .shortdesc}
{:script: data-hd-video='script'}
{:support: data-reuse='support'}
{:table: .aria-labeledby="caption"}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:help: data-hd-content-type='help'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:java: .ph data-hd-programlang='java'}
{:javascript: .ph data-hd-programlang='javascript'}
{:swift: .ph data-hd-programlang='swift'}
{:curl: .ph data-hd-programlang='curl'}
{:video: .video}
{:step: data-tutorial-type='step'}
{:tutorial: data-hd-content-type='tutorial'}
{:ui: .ph data-hd-interface='ui'}
{:cli: .ph data-hd-interface='cli'}
{:api: .ph data-hd-interface='api'}

# Twistlock
{: #setup-twistlock}

You can prevent risk by stopping the deployment of vulnerable images in your environment. With automated and custom policy enforcement, [Twistlock](https://www.twistlock.com){: external} offers complete control at every stage of the application lifecycle.
{: shortdesc}

When you configure the business partner connection, two cards are created in your dashboard that summarize the findings from Twistlock.

| Card                      | Description of findings   |
|:--------------------------|:--------------------------|
| Twistlock runtime         | Total incidents and audits: Findings that are related to incidents or audits on your cloud-native workloads. </br>Total firewall audits: Findings that are related to issues with your firewall. |
| Twistlock Vulnerabilities | Total images with new vulnerabilities: Findings that are related to vulnerabilities found in your container images. |
{: caption="Table 1. Summary of cards that are generated when you connect your Twistlock account" caption-side="top"}


## Before you begin
{: #twistlock-before}

Before you start integrating business partners, be sure that you have the following prerequisites:

* An account with the business partner that you want to integrate.
* The required permissions to obtain the registration URL from the business partner.
* The IAM role `administrator` for the {{site.data.keyword.security-advisor_short}} and {{site.data.keyword.compliance_short}} services.


## Configuring Twistlock
{: #configure-twistlock}

You can use the {{site.data.keyword.compliance_short}} UI to create a connection to Twistlock. When the connection is created, you:

* Establish trust and associate your {{site.data.keyword.cloud_notm}} and business partner accounts
* Copy the required information such as credentials and URLs between the accounts
* Install the business partner's finding metadata into Security Insights
* Validate the pairing by posting a finding from the business partner into Security Insights

1. In the {{site.data.keyword.cloud_notm}} console, click the **Menu** icon ![Menu icon](../icons/icon_hamburger.svg) **> Security and compliance** to access the {{site.data.keyword.compliance_short}}.
2. Navigate to **Gain insight > Configure > Business partners**.
3. On the **Twistlock** tile, click **Connect**.
4. Provide a name for your connection.
5. Input the registration URL provided by Twistlock. If you don't know the URL, click **Get URL from Twistlock** to go to your Twistlock account and use the following steps to retrieve the URL.
  1. In the Twistlock dashboard, navigate to **Manage > Alerts > Add profile**.
  2. Select {{site.data.keyword.security-advisor_short}} from the Provider drop down.
  3. Copy the available URL.
6. Click **Connect**.


## Verifying the connection
{: #twistlock-verify}

1. In the Insights overview, check to see whether the Twistlock cards are displaying as expected.
2. In the Twistlock dashboard, refresh the **Alerts** tab. The {{site.data.keyword.security-advisor_short}} connection shows. Open the connection.
3. Verify that the alert types that you want to be notified of are checked and then click **Verify**.

