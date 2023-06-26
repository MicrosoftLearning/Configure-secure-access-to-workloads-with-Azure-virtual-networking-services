---
lab:
    title: 'Exercise: Control the network traffic to and from the web application'
    module: 'Guided Project - Configure secure access to workloads with Azure virtual networking services'
---

# Lab: Control the network traffic to and from the web application


## Scenario

Your organization requires control of the network traffic to and from the web application. To further enhance the security of the web application, network security groups (NSG) and application security groups (ASG) can be configured. NSG is a security layer that filters network traffic to and from Azure resources, while ASG allows grouping of resources to be managed collectively. These security groups provide fine-grained control over the network traffic to and from the web application components.


### Architecture diagram

![Diagram that shows one ASG and NSG associated to a virtual network.](../Media/task-2.png)

### Skilling tasks
- Create an NSG.
- Create NSG rules.
- Associate an NSG to a subnet.
- Create and use Application Security Groups in NSG rules.

## Exercise instructions

1. Create a new **application security group** named **app-backend-asg** in the **East US** region by using the **RG1** resource group. [Learn more about creating an application security group](https://docs.microsoft.com/azure/virtual-network/tutorial-filter-network-traffic#create-application-security-groups).

>**Note**: You are creating the application security group in the same region as the existing virtual network. 

 
1. Create a **network security group** named **app-vnet-nsg** in **RG1** resource group. [Learn more about creating a network security group](https://docs.microsoft.com/azure/virtual-network/tutorial-filter-network-traffic#create-a-network-security-group).

1. Associate the **app-vnet-nsg** to the **backend** subnet in the **app-vnet**. [Learn more about creating a network security group](https://docs.microsoft.com/azure/virtual-network/tutorial-filter-network-traffic#create-a-network-security-group).

1. Create an inbound security rule named **AllowSsh** in the **app-vnet-nsg** network security group to allow incoming **TCP** traffic on **port 22** to reach the **app-backend-asg** application security group. For any property that is not specified, use the default value. [Learn more about creating a network security group rule](https://docs.microsoft.com/azure/virtual-network/tutorial-filter-network-traffic#create-a-network-security-group).

1. Verify that both the **VM1** and **VM2** virtual machines are running.

1. Verify that you have created an application security group named **app-backend-asg**.

1. Associate the **app-backend-asg** application security group to the **VM2-nic** network interface that is attached to **VM2**. [Learn more about adding a NIC to an application security group](https://learn.microsoft.com/en-us/azure/virtual-network/virtual-network-network-interface?tabs=azure-portal#add-or-remove-from-application-security-groups).

1. Verify that you have associated the application security group to the **VM2-nic** that is attached to **VM2**.

1. Verify that you have configured the **AllowSSH** incoming security rule to use **app-backend-asg** as the destination.
