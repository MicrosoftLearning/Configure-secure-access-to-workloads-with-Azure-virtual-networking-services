---
demo:
    title: 'Demonstration: Create and configure network security groups'
    module: 'Guided Project - Configure secure access to workloads with Azure virtual networking services'
---
## Demonstration – Create and configure network security groups


In this demonstration, we will explore security groups. 

[Restrict access to PaaS resources - tutorial - Azure portal](https://docs.microsoft.com/azure/virtual-network/tutorial-restrict-network-access-to-resources)

### Create a network security group

1. Access the Azure Portal.

1. Search for and select the **Network Security Groups**.

1. Create a NSG explaining the settings as you go. 
 
1. Wait for the new NSG to deploy.

**Explore inbound and outbound rules**

1. Select your new NSG.

1. Discuss how the NSG can be associated with subnets or network interfaces.

1. Discuss the purpose inbound and outbound rules.  

1. Review the default inbound and outbound rules. 

1. Create a new rule, explaining the settings as you go. Specifically discuss the service selection (like HTTPS) and the priority settings. 
 

### Configure ASGs
 [Supporting Slide]

### Associate the NSGs 
8.	Navigate to the NSG you created
9.	Select Subnets from the Settings section.
10.	In the Subnets page, select + Associate
11.	Under Associate subnet, select your Virtual network.


>**Note**: Students should now be able to complete LAB_02

