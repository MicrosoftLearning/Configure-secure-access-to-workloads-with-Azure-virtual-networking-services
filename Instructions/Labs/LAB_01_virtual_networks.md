---
lab:
    title: 'Exercise: Provide network isolation and segmentation for the web application'
    module: 'Guided Project - Configure secure access to workloads with Azure virtual networking services'
---

# Lab: Provide network isolation and segmentation for the web application

## Scenario

The IT department needs network isolation and segmentation for the web application. To provide network isolation and segmentation for the web application, you need to create an Azure virtual network with subnets that the IT team provided. Once the virtual network is created, the next step is to configure virtual network peering. This allows the virtual networks to communicate with each other securely and privately.

### Architecture diagram

![Diagram that shows two virtual networks that are peered.](../Media/task-1.png)

### Skilling tasks

- Create a virtual network
- Create a subnet
- Configure vnet peering

## Exercise instructions

>**Note**: To complete this lab you will need an [Azure subscription](https://azure.microsoft.com/free/) with **Contributor** RBAC role assigned.
> In this lab, when you are asked to create a resource, for any properties that are not specified, use the default value.

### Create Virtual Networks and subnets

Begin by creating the networks shown in the diagram above.

1. Open a browser and navigate to the <a href="https://portal.azure.com/#home">Azure portal</a> and login.
1. To create a Virtual Network, in the search bar at the top of the portal type **"Virtual Networks"** and select **"Virtual Networks"** from the results.
1. In the **"Virtual Networks"** portal pane, select ""**+ Create**".
1. Fill out all the tabs of the creation process by using the values in the following table:

    | Property             | Value           |
    | :------------------- | :-------------- |
    | Resource group       | **RG1**         |
    | Name                 | **app-vnet**    |
    | Region               | **East US**     |
    | IPv4 address space   | **10.1.0.0/16** |
    | Subnet name          | **frontend**    |
    | Subnet address range | **10.1.0.0/24** |
    | Subnet name          | **backend**     |
    | Subnet address range | **10.1.1.0/24** |

    **Note**: Leave all other settings as their defaults. Select **"Next"** to advance to the next tab, and **Create** to create the virtual network.
1. Following the same steps as above, create the Azure virtual network **shared-services-vnet** by using the values in the following table:

    | Property             | Value                    |
    | :------------------- | :----------------------- |
    | Resource group       | **RG1**                  |
    | Name                 | **shared-services-vnet** |
    | Region               | **East US**              |
    | IPv4 address space   | **10.0.0.0/16**          |
    | Subnet name          | **frontend**             |
    | Subnet address range | **10.0.0.0/24**          |

1. Once the deployment is complete. Navigate back to the portal, in the search bar type **"resource groups"** and select **Resource Groups"** from the results. Select on **"RG1"** in the main pane and comfirm both virtual networks have been deployed.

### Setup a peer relationship between the virtual networks

1. Setting up a peer relationship between the two virtual networks will allow traffic to flow in both directions between the **app-vnet** and **shared-services-vnet** virtual networks.
1. In the Portal in the RG1 resource group view. Select on the **"app-vnet"** virtual network.
1. On the **app-vnet** context menu on the left hand side of the portal scroll down and select on **peerings**
1. In the **app-vnet** peerings pane, Select **+ Add**.
1. Fill out the form using the values in the following table:

    | Property                                 | Value                          |
    | :--------------------------------------- | :----------------------------- |
    | This virtual network Peering link name   | **app-vnet-to-sharedservices** |
    | Remote virtual network Peering link name | **sharedservices-to-app-vnet** |
    | Virtual network                          | **shared-services-vnet**       |

    **Note**: Leave all other settings as their defaults. Select **"Add"** to create the virtual network peering.

    [Learn more about Virtual Network Peering](https://learn.microsoft.com/azure/virtual-network/virtual-network-manage-peering?tabs=peering-portal)

1. Once the process completes,and after the configuration updates. Validate that the **Peering status** is set to **Connected**. (you may have to refresh the page to see the updated status)
