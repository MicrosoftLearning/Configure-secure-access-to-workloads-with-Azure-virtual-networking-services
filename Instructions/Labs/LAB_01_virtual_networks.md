![ClipWindowsGIF](https://github.com/MicrosoftLearning/Configure-secure-access-to-workloads-with-Azure-virtual-networking-services/assets/62559534/26fb0421-6837-46d1-af0f-9efc8b4351f4)---
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


>**Note**: To complete this lab you will need an [Azure subscription](https://azure.microsoft.com/free/).
> In this lab, when you are asked to create a resource, for any properties that are not specified, use the default value.

1. Create the Azure virtual network **app-vnet** by using the values in the following table:


    | Property | Value    |
    |:---------|:---------|
    |Resource group|**RG1**|
    |Name|	**app-vnet**|
    |Region| **East US**|
    |IPv4 address space|	**10.1.0.0/16**|
    |Subnet name|	**frontend**|
    |Subnet address range|	**10.1.0.0/24**| 
    |Subnet name|	**backend**|
    |Subnet address range|	**10.1.1.0/24**| 

1. Create the Azure virtual network **shared-services-vnet** by using the values in the following table:

    | Property | Value    |
    |:---------|:---------|
    |Resource group|**RG1**|
    |Name|	**shared-services-vnet**|
    |Region| **East US**|
    |IPv4 address space|	**10.0.0.0/16**|
    |Subnet name|	**frontend**|
    |Subnet address range|	**10.0.0.0/24**| 


1. Confirm both virtual networks have deployed.

1. Peer the two virtual networks to allow traffic to flow in both directions between the **app-vnet** and **shared-services-vnet** virtual networks. Use the values in the following table: 

    | Property | Value    | 
    |:---------|:---------|
    |Peering link name|**app-vnet-to-sharedservices**|
    |Peering link name | **sharedservices-to-app-vnet**|

    [Learn more about Virtual Network Peering](https://learn.microsoft.com/azure/virtual-network/virtual-network-manage-peering?tabs=peering-portal)

1. Verify that the peering status of both VNets is Connected.

