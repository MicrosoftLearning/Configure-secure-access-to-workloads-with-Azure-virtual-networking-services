---
lab:
    title: 'Exercise: Record and resolve domain names internally'
    module: 'Guided Project - Configure secure access to workloads with Azure virtual networking services'
---

# Lab: Record and resolve domain names internally

## Scenario

Your organization requires workloads to record and resolve domain names internally in virtual networks. Virtual machines in virtual networks can use domain name instead of IPs for internal communication. In that case, the domain names will be resolved with a private DNS zone through a virtual network link. 



### Architecture diagram

![Diagram of Azure DNS linked to a virtual network.](../Media/task-5.png)

### Skilling tasks
- Create and configure a private DNS zone. 
- Create and configure DNS records.
- Configure DNS settings on a virtual network.

## Exercise instructions


1. Create a private DNS Zone named ****Contoso.com**** in the ****RG1**** resource group. 

1. Create a Virtual Network Link within the private DNS Zone to the **app-vnet** named ****app-vnet-link**** with auto registration enabled.

1. Create a DNS record set for VM2 named **backend** that is Type A with IP address **10.1.1.4** 

1. Verify that **contoso.com** has a record set named **backend**
