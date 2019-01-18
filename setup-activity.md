---

copyright:
  years: 2017, 2019
lastupdated: "2019-01-18"

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


# Enabling Activity Insights
{: #setup}

With {{site.data.keyword.security-advisor_long}}, you can continuously monitor your IBM Cloud Activity Tracker logs to identify unauthorized or suspicious behavior and changes in your resources. You can use rule packages that are based on best practices that are provided by the service or create your own custom rules.
{: shortdesc}


## Before you begin
{: #prereq}

To get started with Activity Insights, be sure that you have the following prerequisites:

- For Windows 10, activate Windows Subsystem for Linux and install an [Ubuntu shell](https://win10faq.com/install-run-ubuntu-bash-windows-10/)
- Install the yq CLI
  - For MacOS, Windows 10: Install [yq CLI](http://mikefarah.github.io/yq/)
  - For CentOS, Red Hat and Ubuntu : Install yq CLI version 1.15 by running the following commands:
    ```
    wget https://github.com/mikefarah/yq/releases/download/1.15.0/yq_linux_amd64       
    mv yq_linux_amd64 yq   
    chmod +x yq    
    mv yq /usr/local/bin/     
    yq -V
    ```
    {: codeblock}     
- cURL binary and ensure that it's updated.
  - For CentOS and Red Hat, you can update by running: `yum update -y nss curl libcurl`
- The [IBM Cloud CLI and required plugins](/docs/cli/index.html#overview)
- The [Kubernetes CLI (kubectl)](https://kubernetes.io/docs/tasks/tools/install-kubectl/) v1.10.11 or higher
- The [Kubernetes Helm (package manager)](/docs/containers/cs_integrations.html#helm) v2.9.0 or higher.
- A standard Kubernetes cluster version 1.7 or higher


</br>

## Creating a COS bucket
{: #setup-guide}

By using the {{site.data.keyword.security-advisor_short}} GUI, you can create a new COS instance and bucket.

1. Navigate to the **Integrations** tab of the service dashboard.

2. Toggle **Analysis Disabled** in the Activity Insights box to **Analysis Enabled**.

3. Click **Go to set up**.

4. In the prerequisites section, click **Create COS instance and bucket**. Your COS instance and bucket are automatically created for you with the proper naming convention and IAM permissions. The bucket information is displayed.

If you have an existing instance of COS and bucket be sure that it uses the naming convention: `sa.<account_id>.telemetric.<cos_region>`. To allow the service to read the data that is stored in your COS instance, set up service-to-service authorization by using IBM Cloud IAM. Set `source` to `Security Advisor` and `target` to your COS instance. Assign the `Reader` IAM role.

</br>

## Installing {{site.data.keyword.security-advisor_short}} components
{: #install-components}

You can install an agent to collect network flow logs from your Kubernetes cluster. The logs are stored in your Cloud Object Storage instance. You can then enable Network Insights to analyze your logs and detect and alert you to suspicious network activity.
{: shortdesc}

1. Clone the following repository to your local system.

  ```
  https://github.ibm.com/security-services/security-advisor-activity-insights-installer.git
  ```
  {: codeblock}

2. Change into the *security-advisor-activity-insights-installer* folder.

3. Extract the `.tar` file by running the following command.

  ```
  tar -xvf security-advisor-activity-insights.tar
  ```
  {: codeblock}

4. Change into *security-advisor-activity-insights** folder.

5. Run the following command to install the Insights. The command validates your bucket naming convention, creates Kubernetes secrets, updates the values with your cluster GUID, and deploys Activity Insights. If you encounter an error, try running `helm init --upgrade`.

  ```
  ./activity-insight-install.sh <cos_region> <cos_api_key> <at_region> <account_api_key> <account_spaces> <us_south_region_token>
  ```
  {: codeblock}

  <table>
    <tr>
      <th>Variable</th>
      <th>Description</th>
    </tr>
    <tr>
      <td><code>cos_region</code></td>
      <td>The region where your COS instance is deployed. Options include: <code>us-south</code> and <code>eu-gb</code>.</td>
    </tr>
    <tr>
      <td><code>cos_api_key</code></td>
      <td>The API key that you created to access your COS instance and bucket. The key must have the platform role `writer`.</td>
    </tr>
    <tr>
      <td><code>at_region</code></td>
      <td>The region in which you created your COS instance and bucket. Options include: <code>us-south</code> and <code>eu-gb</code>.</td>
    </tr>
    <tr>
      <td><code>account_api_key</code></td>
      <td>The platform API key for your IBM Cloud account.</td>
    </tr>
    <tr>
      <td><code>account_spaces</code></td>
      <td>A comma separated list of the space GUIDs for your IBM Cloud account.</td>
    </tr>
    <tr>
      <td><code>us_south_region_token</code></td>
      <td>Optional: SHAWNA: what is this?. If the cluster is located in the <code>eu-gb</code> region, then create a Container Registry token in the <code>us-south</code> region and pass it to the other region.</td>
    </tr>
  </table>

6. Check to see that the cards in the service dashboard are showing correctly to verify that your setup was successful.

</br>

## Adding rule packages to COS
{: #adding-rules}

A rule package is a JSON file that contains a list of rules that you want to monitor. You can download rule packages or [create your own](rules.html). The Security Advisor engine validates that each rule follows the correct syntax.
{: shortdesc}

1. Clone the following repository to get several preset rule packages.

  ```
  https://github.ibm.com/security-services/security-advisor-ata-rule-packages
  ```
  {: codeblock}

2. Install the package into your COS bucket in `IBM.rules/activities`.

SHAWNA: How do you actually do this?
{: important}

</br>

## Deleting the components
{: #delete}

If you no longer have a need to use Activity Insights, you can delete the service components from your cluster.
{: shortdesc}

1. Delete the service components by using Helm.

  ```
  helm del --purge activity-insights
  ```
  {: codeblock}

2. Delete the Kubernetes secrets.

  ```
  kubectl delete ns security-advisor-insights
  ```
  {: codeblock}

</br>
</br>

</staging>