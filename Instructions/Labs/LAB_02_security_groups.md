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

[Application security groups (ASGs)](https://learn.microsoft.com/azure/virtual-network/application-security-groups) let you group together servers with similar functions. For example, all the web servers hosting your application. 

1. In the portal, search for and select `Application security groups`.
   
1. Select **+ Create** and configure the application security group. 

    | Property       | Value                        |
    | :------------- | :--------------------------- |
    | Subscription   | **Select your subscription** |
    | Resource group | **RG1**                      |
    | Name           | `app-backend-asg`          |
    | Region         | **East US**                  |

1. Select **Review + create** and then select **Create**.

>**Note**: You are creating the application security group in the same region as the existing virtual network.

### Create and Associate the Network Security Group

[Network security groups (NSGs)](https://learn.microsoft.com/azure/virtual-network/network-security-groups-overview) secure network traffic in a virtual network. 

1. In the portal search for and select `Network security group`.

1. Select **+ Create** and configure the network security group. 

    | Property       | Value                        |
    | :------------- | :--------------------------- |
    | Subscription   | **Select your subscription** |
    | Resource group | **RG1**                      |
    | Name           | `app-vnet-nsg`            |
    | Region         | **East US**                  |

1. Select **Review + create** and then select **Create**.

**Associate the NSG with the app-vnet backend subnet.**

NSGs can be associated with subnets and/or individual network interfaces attached to Azure virtual machines. 

1. Select **Go to resource** or navigate to the **app-vnet-nsg** resource.

1. In the **Settings** blade select **Subnets**.

1. Select **+ Associate**

1. Select **app-vnet (RG1)** and then the **Backend** subnet. Select **OK**.

### Create Network Security Group rules

An NSG use [security rules](https://learn.microsoft.com/azure/virtual-network/network-security-group-how-it-works) to filter inbound and outbound network traffic. 

1. In the search box at the top of the portal, enter **Network security group**. Select Network security groups in the search results.

1. Select **app-vnet-nsg** from the list of network security groups.

1. In the **Settings** blade, select **Inbound security rules**.

1. Select **+ Add** and configure an inbound security rule. 

    | Property                               | Value                          |
    | :------------------------------------- | :----------------------------- |
    | Source                                 | **Any**                        |
    | Source port ranges                     | **\***                         |
    | Destination                            | **Application Security group** |
    | Destination application security group | **app-backend-asg**            |
    | Service                                | **SSH**                        |
    | Action                                 | **Allow**                      |
    | Priority                               | **100**                        |
    | Name                                   | **AllowSSH**                   |

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
  
1. In the portal search for and select `virtual machines`. 

1. Verify both vm1 and vm2 are **Running**.

### Associate the application security group to the network interface of the VM

When you created the VMs, Azure created a network interface for each VM, and attached it to the VM.

Add the application security group you created previously to the network interface of VM2.

1. In the Azure portal, navigate to the **RG1** resource group and select **VM2**.

1. Navigate to the networking tab of the VM, select **+ Add application security groups** from the **Application security groups** section.

1. Select **app-backend-asg** from the list of application security groups.

1. Select **Add**.
