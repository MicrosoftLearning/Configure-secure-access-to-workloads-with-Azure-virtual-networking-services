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

### Create a private DNS zone

Azure Private DNS provides a reliable, secure DNS service to manage and resolve domain names in a virtual network without the need to add a custom DNS solution. By using private DNS zones, you can use your own custom domain names rather than the Azure-provided names available today.

1. On the portal search bar, type **Private dns zones** in the search text box and select Private DNS zones from the results.

1. Select **+ Create**.

1. On the **Basics** tab of Create private DNS zone, enter the information as listed in the table below:

    | Property | Value    |
    |:---------|:---------|
    |Subscription|**Select your subscription**|
    |Resource group|**RG1**|
    |Name|**contoso.com**|
    |Region|**East US**|

1. Select **Review + create** and then select **Create**.

### Create a virtual network link to your private DNS zone

1. On the portal search bar, type **Private dns zones** in the search text box and select Private DNS zones from the results.

1. Select **contoso.com**.

1. Select **+ Virtual network link**.

1. Select **+ Add"**

1. On the **Basics** tab of Create virtual network link, enter the information as listed in the table below:

    | Property | Value    |
    |:---------|:---------|
    |Link name|**app-vnet-link**|
    |Virtual network|**app-vnet**|
    |Enable auto registration|**Enabled**|

1. Select **OK**

### Create a DNS record set

1. On the portal search bar, type **Private dns zones** in the search text box and select Private DNS zones from the results.

1. Select **contoso.com**.

1. Select **+ Record set**.

1. On the **Basics** tab of Create record set, enter the information as listed in the table below:

    | Property | Value    |
    |:---------|:---------|
    |Name|**backend**|
    |Type|**A**|
    |TTL|**1**|
    |IP address|**10.1.1.4**|


1. Select **OK**

1. Verify that **contoso.com** has a record set named **backend**
