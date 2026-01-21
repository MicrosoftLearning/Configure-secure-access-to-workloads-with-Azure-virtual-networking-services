---
lab:
    title: 'Exercise 03: Create and configure Azure Firewall'
    module: 'Guided Project - Configure secure access to workloads with Azure virtual networking services'
---

# Exercise 03: Create and configure Azure Firewall

## Scenario

Your organization requires centralized network security for the application virtual network. As the application usage increases, more granular application-level filtering and advanced threat protection will be needed. Also, it is expected the application will need continuous updates from Azure DevOps pipelines. You identify these requirements.
+ Azure Firewall is required for additional security in the app-vnet. 
+ A **firewall policy** should be configured to help manage access to the application. 
+ A firewall policy **application rule** is required. This rule will allow the application access to Azure DevOps so the application code can be updated. 
+ A firewall policy **network rule** is required. This rule will allow DNS resolution. 

### Skilling tasks

+ Create an Azure Firewall.
+ Create and configure a firewall policy
+ Create an application rule collection.
+ Create a network rule collection.

## Architecture diagram

![Diagram that shows one virtual network with a firewall and route table.](../Media/task-3.png)

## Estimated timing: 25 minutes
  
## Exercise instructions

### Create  Azure Firewall subnet in our existing virtual network

1. In the search box at the top of the portal, enter **Virtual networks**. Select **Virtual networks** in the search results.

1. Select **app-vnet**.

1. Select **Subnets**.

1. Select **+ Subnet**.

1. Enter the following information and select **Save**.

    | Property      | Value                   |
    | :------------ | :---------------------- |
    | Name          | **AzureFirewallSubnet** |
    | Address range | **10.1.63.0/26**        |

**Note**: Leave all other settings as default.

### Create an Azure Firewall

1. In the search box at the top of the portal, enter **Firewall**. Select **Firewall** in the search results.

1. Select **+ Create**.

1. Create a firewall by using the values in the following table. For any property that is not specified, use the default value.
    >**Note**: Azure Firewall can take a few minutes to deploy.

    | Property                 | Value                                             |
    | :----------------------- | :------------------------------------------------ |
    | Resource group           | **RG1**                                           |
    | Name                     | **app-vnet-firewall**                             |
    | Firewall SKU             | **Standard**                                      |
    | Firewall management      | **Use a Firewall Policy to manage this firewall** |
    | Firewall policy          | select **Add new**                                |
    | Policy name              | **fw-policy**                                     |
    | Region                   | **East US**                                       |
    | Policy Tier              | **Standard**                                      |
    | Choose a virtual network | **Use existing**                                  |
    | Virtual network          | **app-vnet** (RG1)                                |
    | Public IP address        | Add new: **fwpip**                                |
    | Enable Firewall Management NIC | **uncheck the box**                         |

    [Learn more on creating a firewall](https://docs.microsoft.com/azure/firewall/tutorial-firewall-deploy-portal).

1. Select **Review + create** and then select **Create**.

### Update the Firewall Policy

1. In the portal, search for and select `Firewall Policies`. 

1. Select **fw-policy**.

### Add an application rule

1. In the **Settings** blade, select **Application rules** and then **Add a rule collection**.

1. Configure the application rule collection and then select **Add**. 

    | Property               | Value                                     |
    | :--------------------- | :---------------------------------------- |
    | Name                   | `app-vnet-fw-rule-collection`         |
    | Rule collection type   | **Application**                           |
    | Priority               | `200`                                   |
    | Rule collection action | **Allow**                                 |
    | Rule collection group  | **DefaultApplicationRuleCollectionGroup** |
    | Name             | `AllowAzurePipelines`                |
    | Source type      | **IP address**                         |
    | Source           | `10.1.0.0/23`                       |
    | Protocol         | `https`                             |
    | Destination type | **FQDN**                                  |
    | Destination      | `dev.azure.com, azure.microsoft.com` |

**Note**: The **AllowAzurePipelines** rule allows the web application to access Azure Pipelines. The rule allows the web application to access the Azure DevOps service and the Azure website.

### Add a network rule

1. In the **Settings** blade, select **Network rules** and then **Add a network collection**.

1. Configure the network rule and then select **Add**.  

    | Property               | Value                                 |
    | :--------------------- | :------------------------------------ |
    | Name                   | `app-vnet-fw-nrc-dns`               |
    | Rule collection type   | **Network**                           |
    | Priority               | `200`                        |
    | Rule collection action | **Allow**                             |
    | Rule collection group  | **DefaultNetworkRuleCollectionGroup** |
    | Rule                  | **AllowDns**         |
    | Source                | `10.1.0.0/23`      |
    | Protocol              | **UDP**              |
    | Destination ports     | `53`               |
    | Destination addresses | **1.1.1.1, 1.0.0.1** |

### Verify the firewall and firewall policy status

1. In the portal search for and select **Firewall**. 

1. View the **app-vnet-firewall** and ensure the **Provisioning state** is **Succeeded**. This may take a few minutes. 

1. In the portal serach for and select **Firewall policies**.

1. View the **fw-policy** and ensure the **Provisioning state** is **Succeeded**. This may take a few minutes.

### Learn more with online training

+ [Introduction to Azure Firewall](https://learn.microsoft.com/training/modules/introduction-azure-firewall/). In this module, you learn about how Azure Firewall features, rules, deployment options, and administration.
+ [Introduction to Azure Firewall Manager](https://learn.microsoft.com/training/modules/intro-to-azure-firewall-manager/). In this moudle, you learn how Azure Firewall Manager provides central security policy and route management for cloud-based security perimeters.

### Key takeaways

Congratulations on completing the exercise. Here are the main takeaways:

+ Azure Firewall is a cloud-based security service that protects your Azure virtual network resources from incoming and outgoing threats.
+ An Azure firewall policy is a resource that contains one or more collections of NAT, network, and application rules.
+ Network rules allow or deny traffic based on IP addresses, ports, and protocols.
+ Application rules allow or deny traffic based on fully qualified domain names (FQDNs), URLs, and HTTP/HTTPS protocols.
