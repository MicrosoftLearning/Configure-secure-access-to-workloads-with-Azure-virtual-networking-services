---
demo:
    title: 'Demonstration: Create and Configure Virtual Networks and peering'
    module: 'Guided Project - Configure secure access to workloads with Azure virtual networking services'
---
## Demonstration – Create and Configure Virtual Networks and peering


In this demonstration, you will create virtual networks.

**Note:** You can use the suggested values for the settings, or your own custom values if you prefer.

[Quickstart: Create a virtual network - Azure portalk](https://docs.microsoft.com/azure/virtual-network/quick-create-portal)

### Create a virtual network in the portal

1.  Sign in the to the Azure portal and search for **Virtual Networks**.

1.  Create a virtual network, explaining the basic settings as you go. Ensure at least one subnet is created. 

1.  Verify your virtual network was created.

In this demonstration, we will explore virtual networks. 
1.  [Supporting Slide] Before beginning the demonstration, let's review what virtual networks are and key concepts for Azure Virtual Networks. Use this slide to highlight the capabilities of Azure Virtual Networks. As well as Azure Virtual Network concepts and best practices. As you demonstrate creating a virtual network you can explain the basic concepts of address space, subnets, regions, and subscriptions. You could also discuss these slides at the end and get straight into the demonstration.
 
2.	Access the Azure portal.
3.	In the search box, type Virtual Network. As you begin typing, the list filters based on your input.
4.	Select Virtual Network.
5.	Click Create.
6.	Explain the Azure portal provides an easy-to-use interface. Items marked with a red asterisk are required.
7.	Select the available subscription.
8.	Select the available resource group.
9.	Enter a name for your virtual network. Point out the opportunity for naming conventions.
10.	[Supporting Slide] Select a region for your network. Use this slide to discuss Azure geographies. 
11. [Supporting Slide] Select the Security tab. Use this slide to highlight the security services briefly, these topics will be covered in more detail later in the course. Learn more, Services that can be deployed into a virtual network. 
    
>**Note**: Note we are only covering a few things to get the student started on their first lab.   

12.	[Supporting Slide] Select the IP Addresses tab. Use this slide to review: Plan virtual networks and subnets. Add or modify a subnet to demonstrate to students how to configure subnets. 
13.	Click Review and ensure there are no validation errors.
14.	Click Create and wait for the virtual network to be deployed. Point out the notification messages. 
15.	Show how to go to the resource.
16.	Repeat the process of creating another virtual network so you can demonstrate VNet Peering.

## Configure VNet Peering

**Note:** For this demonstration you will need two virtual networks.

[Connect virtual networks with VNet peering - tutorial](https://docs.microsoft.com/azure/virtual-network/tutorial-connect-virtual-networks-portal)

**Configure VNet peering on the first virtual network**

1. In the **Azure portal**, select the first virtual network. Review the value of peering. 

1. Under **Settings**, select **Peerings** and **+ Add** a new peering.

1. Configure the peering the second virtual network. Use the information icons to review the different settings. 

1. When the peering is complete, review the **Peering status**. 

**Confirm VNet peering on the second virtual network**

1. In the **Azure portal**, select the second virtual network

1. Under **Settings**, select **Peerings**.

1. Notice that a peering has automatically been created. Notice that the **Peering Status** is **Connected**.


>**Note**: Students should now be able to complete LAB_01

