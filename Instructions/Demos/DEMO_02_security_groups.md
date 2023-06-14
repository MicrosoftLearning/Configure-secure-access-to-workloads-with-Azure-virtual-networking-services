---
demo:
    title: 'Demonstration: Create and configure network security groups'
    module: 'Guided Project - Configure secure access to workloads with Azure virtual networking services'
---
## Demonstration – Create and configure network security groups


In this demonstration, we will explore security groups. 

**Note:** An **[interactive lab simulation for virtual networks](https://mslearn.cloudguides.com/en-us/guides/AZ-900%20Exam%20Guide%20-%20Azure%20Fundamentals%20Exercise%2013?azure-portal=true)** is available that allows you to click through a similar lab if you are unable to do a live demonstration. You may find slight differences between the interactive simulation and the suggested demo, but the core concepts and ideas being demonstrated are the same. 

[Restrict access to PaaS resources - tutorial - Azure portal](https://docs.microsoft.com/azure/virtual-network/tutorial-restrict-network-access-to-resources)

### Create a network security group

1. Access the Azure Portal.

1. Search for and select the **Network Security Groups**.

1. [Supporting Slide] Create a NSG explaining the settings as you go. 
 
1. Wait for the new NSG to deploy.

**Explore inbound and outbound rules**

1. Select your new NSG.

1. [Supporting Slide] Discuss how the NSG can be associated with subnets or network interfaces.

1. Discuss the purpose inbound and outbound rules.  

1. Review the default inbound and outbound rules. 

1. Create a new rule, explaining the settings as you go. Specifically discuss the service selection (like HTTPS) and the priority settings. 
 

### Create ASG
 
1. [Supporting Slide] Search for and select the **Application Security Groups**.

1. Create an ASG explaining the settings as you go. 
 
1. Wait for the new ASG to deploy.

1. Discuss how the ASG can be associated with NSG rules.


### Associate the NSGs 
1.	Navigate to the NSG you created
1.	Select Subnets from the Settings section.
1.	In the Subnets page, select + Associate
1.	Under Associate subnet, select your Virtual network.


>**Note**: Students should now be able to complete LAB_02

