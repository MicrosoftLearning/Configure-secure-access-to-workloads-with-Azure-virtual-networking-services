---
lab:
    title: 'Exercise 01: Create and configure virtual networks'
    module: 'Guided Project - Configure secure access to workloads with Azure virtual networking services'
---

# Exercise 01: Create and configure virtual networks

## Scenario

Your organization is migrating a web-based application to Azure. Your first task is to put in place the virtual networks and subnets. You also need to securely peer the virtual networks. You identify these requirements.	
+ Two virtual networks are required, **app-vnet** and **hub-vnet**. This simulates a hub and spoke network architecture. 
+ The app-vnet will host the application. This virtual network requires two subnets. The **frontend subnet** will host the web servers. The **backend subnet** will host the database servers.
+ The hub-vnet only requires a subnet for the firewall. 
+ The two virtual networks must be able to communicate with each other securely and privately through **virtual network peering**. 
+ Both virtual networks should be in the same region. 

## Skilling tasks

+ Create a virtual network.
+ Create a subnet.
+ Configure vnet peering.

## Estimated timing: 20 minutes

## Architecture diagram

![Diagram that shows two virtual networks that are peered.](../Media/task-1.png)

## Exercise instructions

**Note**: To complete this lab you will need an [Azure subscription](https://azure.microsoft.com/free/) with **Contributor** RBAC role assigned. In this lab, when you are asked to create a resource, for any properties that are not specified, use the default value.

### Create hub and spoke virtual networks and subnets

An [Azure virtual network](https://learn.microsoft.com/azure/virtual-network/virtual-networks-overview) enables many types of Azure resources to securely communicate with each other, the internet, and on-premises networks. All Azure resources in a virtual network are deployed into [subnets](https://learn.microsoft.com/azure/virtual-network/virtual-network-manage-subnet?tabs=azure-portal) within the virtual network. 

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

    **Note**:Leave all other settings as their defaults. When finished select **"Review + create** and then **Create**.
   
1. Create the **Hub-vnet** virtual network configuration. This virtual network has the firewall subnet. 

    | Property             | Value                    |
    | :------------------- | :----------------------- |
    | Resource group       | **RG1**                  |
    | Name                 | `hub-vnet` |
    | Region               | **East US**              |
    | IPv4 address space   | **10.0.0.0/16**          |
    | Subnet name          | **AzureFirewallSubnet**  |
    | Subnet address range | **10.0.0.0/26**          |

1. Once the deployments are complete, search for and select your 'virtual networks`.

1. Verify your virtual networks and subnets were deployed. 

### Configure a peer relationship between the virtual networks

[Virtual network peering](https://learn.microsoft.com/azure/virtual-network/virtual-network-peering-overview) enables you to seamlessly connect two or more Virtual Networks in Azure. 

1. Search for and select the `app-vnet` virtual network.
   
1. In the **Settings** blade, select **Peerings**.
   
1. **+ Add** a peering between the two virtual networks. 

    | Property                                 | Value                          |
    | :--------------------------------------- | :----------------------------- |
    | Remote peering link name              | `app-vnet-to-hub` |
    | Virtual network    | `hub-vnet` |
    | Local virtual network peering link name | `hub-to-app-vnet` |

    **Note**: Leave all other settings as their defaults. Select **"Add"** to create the virtual network peering.

1. Once the deployment completes, verify the **Peering status** is **Connected**.

## Learn more with online training

+ [Introduction to Azure Virtual Networks](https://learn.microsoft.com/training/modules/introduction-to-azure-virtual-networks/). In this module, you learn how to design and implement Azure networking services. You learn about virtual networks, public and private IPs, DNS, virtual network peering, routing, and Azure Virtual NAT.

## Key takeaways

Congratulations on completing the exercise. Here are the main takeaways:

+ Azure virtual networks (VNets) provide a secure and isolated network environment for your cloud resources. You can create multiple virtual networks per region per subscription.
+ When designing virtual networks make sure the VNet address space (CIDR block) doesn't overlap with your organization's other network ranges.
+ A subnet is a range of IP addresses in the VNet. You can segment VNets into different size subnets, creating as many subnets as you require for organization and security within the subscription limit. Each subnet must have a unique address range.
+ Certain Azure services, such as Azure Firewall, require their own subnet.
+ Virtual network peering enables you to seamlessly connect two Azure virtual networks. The virtual networks appear as one for connectivity purposes.
