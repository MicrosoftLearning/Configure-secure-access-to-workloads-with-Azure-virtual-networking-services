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

### Create Application Security Group

An application security group (ASGs) enables you to group together servers with similar functions, such as web servers.

1. In the search box at the top of the portal, enter **Application security group**. Select Application security groups in the search results.

1. Select **+ Create**.

    On the **Basics** tab of Create an application security group, enter the information as listed in the table below:

    | Property | Value    |
    |:---------|:---------|
    |Subscription|**Select your subscription**|
    |Resource group|**RG1**|
    |Name|**app-backend-asg**|
    |Region|**East US**|

1. Select **Review + create** and then select **Create**.

[Learn more about creating an application security group](https://docs.microsoft.com/azure/virtual-network/tutorial-filter-network-traffic#create-application-security-groups).

>**Note**: You are creating the application security group in the same region as the existing virtual network.

### Create and Associate the Network Security Group

A network security group (NSG) secures network traffic in your virtual network. NSGs contain a list of security rules that allow or deny network traffic to resources connected to Azure Virtual Networks (VNet). NSGs can be associated with subnets and/or individual network interfaces attached to Azure Virtual Machines (VM).

1. In the search box at the top of the portal, enter **Network security group**. Select **Network security groups** in the search results.

1. Select **+ Create**.

    On the **Basics** tab of Create network security group, enter the information as listed in the table below:

    | Property | Value    |
    |:---------|:---------|
    |Subscription|**Select your subscription**|
    |Resource group|**RG1**|
    |Name|**app-vnet-nsg**|
    |Region|**East US**|

    [Learn more about creating a network security group](https://docs.microsoft.com/azure/virtual-network/tutorial-filter-network-traffic#create-a-network-security-group).

1. Select **Review + create** and then select **Create**.

In this section, you associate the network security group with the subnet of the virtual network you created earlier.

1. In the search box at the top of the portal, enter **Network security group**. Select Network security groups in the search results.

1. Select **app-vnet-nsg** from the list of network security groups.

1. Select **Subnets** from the Settings section of **app-vnet-nsg**.

1. In the Subnets page, select **+ Associate**

1. Under **Associate subnet**, select **app-vnet (RG1)** for Virtual network. and select **Backend** for Subnet, and then select OK.

    [Learn more about associating a network security group to a subnet](https://docs.microsoft.com/azure/virtual-network/tutorial-filter-network-traffic#associate-a-network-security-group-to-a-subnet).

### Create Network Security Group rules
A network security group (NSG) secures network traffic in your virtual network.

1. In the search box at the top of the portal, enter **Network security group**. Select Network security groups in the search results.

1. Select **app-vnet-nsg** from the list of network security groups.

1. Select **Inbound security rules** from the Settings section of **app-vnet-nsg**.

1. Select **+ Add**.

1. On the **Add inbound security rule** page, enter the information as listed in the table below:

    | Property | Value    |
    |:---------|:---------|
    |Source|**Any**|
    |Source port ranges|**\***|
    |Destination|**Application Security group**|
    |Destination application security group|**app-backend-asg**|    
    |Service|**SSH**|
    |Action|**Allow**|
    |Priority|**100**|
    |Name|**AllowSSH**|

    [Learn more about creating a network security group rule](https://docs.microsoft.com/azure/virtual-network/tutorial-filter-network-traffic#create-a-network-security-group).

### Deploy an ARM template using Cloud Shell to create the VMs needed for this exercise

1. In the Azure portal, open the **Azure Cloud Shell** by selecting the icon in the top right of the Azure Portal.

1. If prompted to select either **Bash** or **PowerShell**, select **PowerShell**.

    >**Note**: If this is the first time you are starting **Cloud Shell** and you are presented with the **You have no storage mounted** message, select the subscription you are using in this lab, and select **Create storage**.

1. Deploy the following ARM template using Cloud Shell to create the VMs needed for this exercise:

>**Note**: you can select the text in the section below and copy/paste it in the Cloud Shell.

   ```powershell
   $RGName = "RG1"
   
   New-AzResourceGroupDeployment -ResourceGroupName $RGName -TemplateUri https://raw.githubusercontent.com/MicrosoftLearning/Configure-secure-access-to-workloads-with-Azure-virtual-networking-services/main/Instructions/Labs/azuredeploy.json
   ```
  
1. to Verify that both the **VM1** and **VM2** virtual machines are running, navigate to the **RG1** resource group and select **VM1**.

1, Validate that the status of the virtual machine is **Running**.

1. Repeat the previous step for **VM2**.

### Associate the application security group to the network interface of the VM
When you created the VMs, Azure created a network interface for each VM, and attached it to the VM.

Add the network interface of each VM to one of the application security groups you created previously.

1. In the Azure portal, navigate to the **RG1** resource group and select **VM2**.

1. Select **+ Add application security groups** from the **Application security groups** section of **VM2**.

1. Select **app-backend-asg** from the list of application security groups.

1. Select **Add**.

  [Learn more about adding a NIC to an application security group](https://learn.microsoft.com/en-us/azure/virtual-network/virtual-network-network-interface?tabs=azure-portal#add-or-remove-from-application-security-groups).

