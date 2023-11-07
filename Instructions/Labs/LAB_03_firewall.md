---
lab:
    title: 'Exercise: Protect the web application from malicious traffic and block unauthorized access'
    module: 'Guided Project - Configure secure access to workloads with Azure virtual networking services'
---

# Lab: Protect the web application from malicious traffic and block unauthorized access


## Scenario
Your organization is looking to protect the web application from malicious traffic and block unauthorized access.

In addition to NSG and ASG, a firewall can be configured to add an extra layer of security to the web application. A firewall protects the web application from malicious traffic and blocks unauthorized access with policies you configure.

Azure Firewall policy is a top-level resource that contains security and operational settings for Azure Firewall. It allows you to define a rule hierarchy and enforce compliance. In this task you configure application rules and network rules for the firewall using Firewall Policy. You can use Azure Firewall Policy to manage rule sets that the Azure Firewall uses to filter traffic. 

### Architecture diagram

![Diagram that shows one virtual network with a firewall and route table.](../Media/task-3.png)

### Skilling tasks
- Create an Azure Firewall.
- Create and configure a firewall policy
- Create an application rule collection.
- Create a network rule collection.
  
## Exercise instructions

### Create  Azure Firewall subnet in our existing virtual network

1. In the search box at the top of the portal, enter **Virtual networks**. Select **Virtual networks** in the search results.

1. Select **app-vnet**.

1. Select **Subnets**.

1. Select **+ Subnet**.

1. Enter the following information and select **Save**.

    | Property | Value    |
    |:---------|:---------|
    |Name	   | **AzureFirewallSubnet**|
    |Address range|	**10.1.63.0/24**|

    > **Note**: Leave all other settings as default.
    

### Create an Azure Firewall

1. In the search box at the top of the portal, enter **Firewall**. Select **Firewall** in the search results.

1. Select **+ Create**.

1.  Create a firewall by using the values in the following table. For any property that is not specified, use the default value.
    >**Note**: Azure Firewall can take a few minutes to deploy.

    | Property | Value    |
    |:---------|:---------|
    |Resource group   | **RG1**  |
    |Name	   | **app-vnet-firewall**|
    |Firewall SKU |	**Standard**|
    |Firewall management | **Use a Firewall Policy to manage this firewall**|
    |Firewall policy| select **Add new**| 
    |Policy name| **fw-policy**|
    |Region| **East US**|
    |Policy Tier| **Standard**|
    |Choose a virtual network |	**Use existing**|
    |Virtual network | **app-vnet** (RG1)|
    |Public IP address | Add new: **fwpip**|

    [Learn more on creating a firewall](https://docs.microsoft.com/azure/firewall/tutorial-firewall-deploy-portal).

1. Select **Review + create** and then select **Create**.

### Update the Firewall Policy

1. In the search box at the top of the portal, enter **Firewall Policy**. Select **Firewall Policies** in the search results.

1. Select **fw-policy**.

1. Select **Application rules**.

1. Se;ect on **"+ Application rule collection"**.

1. Use the values in the following table. For any property that is not specified, use the default value.

    |Property|	Value |
    |:---------|:---------|
    |Name	|**app-vnet-fw-rule-collection**|
    |Rule collection type| **Application**|
    |Priority|	**200**|
    |Rule collection action|**Allow**|
    |Rule collection group| **DefaultApplicationRuleCollectionGroup**|

    1. Under **rules** use the values in the following table

        |Property|  Value |
        |:---------|:---------|
        |Name	|**AllowAzurePipelines**|
        |Source type|**IP address**|
        |Source|**10.1.0.0/23**|
        |Protocol|**https** |
        |Destination type|FQDN|
        |Destination|**dev.azure.com, azure.microsoft.com**|

        and select **Add**

> **Note**: The **AllowAzurePipelines** rule allows the web application to access Azure Pipelines. The rule allows the web application to access the Azure DevOps service and the Azure website.

1.  Create a **network rule collection** that contains a single IP Address rule by using the values in the following table. For any property that is not specified, use the default value.

1. Select **Network rules**.

1. Select on **"+ Network rule collection"**.

1. Use the values in the following table. For any property that is not specified, use the default value.

    |Property|	Value|
    |:---------|:---------|
    |Name|	**app-vnet-fw-nrc-dns**|
    |Rule collection type| **Network**|
    |Priority|	**200**|
    |Rule collection action|**Allow**|
    |Rule collection group| **DefaultNetworkRuleCollectionGroup**|

    1. Under **rules** use the values in the following table

        |Property|	Value|
        |:---------|:---------|
        |Rule |	**AllowDns**|
        |Source|	**10.1.0.0/23**|
        |Protocol|	**UDP**|
        |Destination ports|	**53**|
        |Destination addresses|	**1.1.1.1, 1.0.0.1**|

        And select **Add**.


    Learn more on [creating an application rule](https://docs.microsoft.com/azure/firewall/tutorial-firewall-deploy-portal#configure-an-application-rule) and [creating a network rule](https://docs.microsoft.com/azure/firewall/tutorial-firewall-deploy-portal#configure-a-network-rule).

1. To verify that the Azure Firewall and Firewall Policy provisioning state show **Succeeded**.

1.In the search box at the top of the portal, enter **Firewall**. Select **Firewall** in the search results.

1. Select **app-vnet-firewall**.

1- Validate that the **Provisioning state** is **Succeeded**.

1- In the search box at the top of the portal, enter **Firewall policies**. Select **Firewall policies** in the search results

1. Select **fw-policy**.

1- Validate that the **Provisioning state** is **Succeeded**.

