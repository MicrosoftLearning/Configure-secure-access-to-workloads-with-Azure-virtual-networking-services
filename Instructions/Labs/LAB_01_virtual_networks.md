---
lab:
    title: 'Exercise: Provide network isolation and segmentation for the web application'
    module: 'Guided Project - Configure secure access to workloads with Azure virtual networking services'
---

# Lab: Provide a shared services hub virtual network with isolation and segmentation

## Scenario

You have been tasked with applying [Zero Trust principles](https://learn.microsoft.com/security/zero-trust/azure-infrastructure-networking) to a hub virtual network in Azure. The IT department needs network isolation and segmentation for the web application in a spoke network. To provide network isolation and segmentation for the web application, you need to create an Azure virtual network with subnets with address space that the IT team provided. Once the virtual network is created, the next step is to configure virtual network peering. This allows the virtual networks to communicate with each other securely and privately.

### Architecture diagram

![Diagram that shows two virtual networks that are peered.](../Media/task-1.png)

### Skilling tasks

- Create a virtual network
- Create a subnet
- Configure vnet peering

## Exercise instructions

>**Note**: To complete this lab you will need an [Azure subscription](https://azure.microsoft.com/free/) with **Contributor** RBAC role assigned.

> In this lab, when you are asked to create a resource, for any properties that are not specified, use the default value.

### Create hub and spoke virtual networks and subnets

Begin by creating the virtual networks shown in the diagram above.

1. Sign in to the **Azure portal** - `https://portal.azure.com`.
   
1. Search for and select `Virtual Networks`.
   
1. Select **+ Create** and complete the configuration of the **app-vnet**. This  virtual network requires two subnets, **frontend** and **backend**. 

    | Property             | Value           |
    | :------------------- | :-------------- |
    | Resource group       | **RG1**         |
    | Virtual network name | `app-vnet`    |
    | Region               | **East US**     |
    | IPv4 address space   | **10.1.0.0/16** |
    | Subnet name          | `frontend`    |
    | Subnet address range | **10.1.0.0/24** |
    | Subnet name          | `backend`     |
    | Subnet address range | **10.1.1.0/24** |

    **Note**: Leave all other settings as their defaults. When finished select **"Review + create** and then **Create**.
   
1. Create the **Hub-vnet** virtual network configuration. This virtual network has the firewall subnet. 

    | Property             | Value                    |
    | :------------------- | :----------------------- |
    | Resource group       | **RG1**                  |
    | Name                 | `hub-vnet` |
    | Region               | **East US**              |
    | IPv4 address space   | **10.0.0.0/16**          |
    | Subnet name          | **AzureFirewallSubnet**  |
    | Subnet address range | **10.0.0.0/26**          |

1. Once the deployments are complete, search for and select your **resource group**. Confirm your new virtual networks are part of the resource group. 

### Configure a peer relationship between the virtual networks

1. Search for and select the `app-vnet` virtual network.
   
1. In the **Settings** blade, select **Peerings**.
   
1. **+ Add** a peering between the two virtual networks. 

    | Property                                 | Value                          |
    | :--------------------------------------- | :----------------------------- |
    | Remote peering link name              | `app-vnet-to-hub` |
    | Virtual network    | `hub-vnet` |
    | Local virtual network peering link name | `hub-to-app-vnet` |

    **Note**: Leave all other settings as their defaults. Select **"Add"** to create the virtual network peering.

    [Learn more about Virtual Network Peering](https://learn.microsoft.com/azure/virtual-network/virtual-network-manage-peering?tabs=peering-portal)

1. Once the deploymnet completes, verify the **Peering status** is **Connected**. 
