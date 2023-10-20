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

1.  Create a subnet named **AzureFirewallSubnet** in the **app-vnet** virtual network by using a subnet address range of **10.1.63.0/24**.

1.  Create a firewall by using the values in the following table. For any property that is not specified, use the default value.
    >**Note**: Azure Firewall can take a few minutes to deploy.

    | Property | Value    |
    |:---------|:---------|
    |Resource group   | **RG1**  |
    |Name	   | **app-vnet-firewall**|
    |Firewall SKU |	Standard|
    |Firewall management | Use a Firewall Policy to manage this firewall|
    |Firewall policy| select **Add new**| 
    |Policy name| **fw-policy**|
    |Region| **East US**|
    |Policy Tier| **Standard**|
    |Choose a virtual network |	Use existing|
    |Virtual network | **app-vnet** (RG1)|
    |Public IP address | Add new: **fwpip**|

    [Learn more on creating a firewall](https://docs.microsoft.com/azure/firewall/tutorial-firewall-deploy-portal), [creating route tables](https://docs.microsoft.com/azure/virtual-network/manage-route-table) and [associating a route table to a subnet](https://docs.microsoft.com/azure/virtual-network/tutorial-create-route-table-portal#associate-a-route-table-to-a-subnet).



1.  Create an **application rule collection** in **fw-policy** that contains a single Target FQDN rule by using the values in the following table. For any property that is not specified, use the default value.

    |Property|	Value |
    |:---------|:---------|
    |Name	|**app-vnet-fw-rule-collection**|
    |Rule collection type| **Application**|
    |Priority|	**200**|
    |Rule collection action|**Allow**|
    |Rule collection group| **DefaultApplicationRuleCollectionGroup**|

1. Under **rules** use the values in the following table and select **Add** 

    |Property|  Value |
    |:---------|:---------|
    |Name	|**AllowAzurePipelines**|
    |Source type|**IP address**|
    |Source|**10.1.0.0/23**|
    |Protocol|**https** |
    |Destination type|FQDN|
    |Destination|**dev.azure.com, azure.microsoft.com**|

1.  Create a **network rule collection** that contains a single IP Address rule by using the values in the following table. For any property that is not specified, use the default value.

    |Property|	Value|
    |:---------|:---------|
    |Name|	**app-vnet-fw-nrc-dns**|
    |Rule collection type| **Network**|
    |Priority|	**200**|
    |Rule collection action|**Allow**|
    |Rule collection group| **DefaultNetworkRuleCollectionGroup**|

1. Under **rules** use the values in the following table and select **Add**    

    |Property|	Value|
    |:---------|:---------|
    |Rule |	**AllowDns**|
    |Source|	**10.1.0.0/23**|
    |Protocol|	**UDP**|
    |Destination ports|	**53**|
    |Destination addresses|	**1.1.1.1, 1.0.0.1**|

    Learn more on [creating an application rule](https://docs.microsoft.com/azure/firewall/tutorial-firewall-deploy-portal#configure-an-application-rule) and [creating a network rule](https://docs.microsoft.com/azure/firewall/tutorial-firewall-deploy-portal#configure-a-network-rule).

1. Verify that the Azure Firewall and Firewall Policy provisioning state show **Succeeded**.


