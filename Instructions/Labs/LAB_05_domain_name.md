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

**Note:** This exercise requires the Lab 01 virtual networks and subnets to be installed. A [template](https://github.com/MicrosoftLearning/Configure-secure-access-to-workloads-with-Azure-virtual-networking-services/blob/main/Allfiles/Labs/02/vnet-subnets-template.json) is provided if you need to deploy those resources.

### Create a private DNS zone

[Azure Private DNS](https://learn.microsoft.com/azure/dns/private-dns-overview) provides a reliable, secure DNS service to manage and resolve domain names in a virtual network without the need to add a custom DNS solution. By using private DNS zones, you can use your own custom domain names rather than the Azure-provided names.

1. On the Azure portal, search for and select `Private dns zones`.

1. Select **+ Create** and configure the DNS zone. 

    | Property       | Value                        |
    | :------------- | :--------------------------- |
    | Subscription   | **Select your subscription** |
    | Resource group | **RG1**                      |
    | Name           | `private.contoso.com`              |
    | Region         | **East US**                  |

1. Select **Review + create** and then select **Create**.

1. Wait for the DNS zone to deploy, and then select **Go to resource**. 

### Create a virtual network link to your private DNS zone

To resolve DNS records in a private DNS zone, resources must  be linked to the private zone. A [virtual network link](https://learn.microsoft.com/azure/dns/private-dns-virtual-network-links) associates the virtual network to the private zone.

1. In the portal, continue working on the **private.contoso.com** DNS zone. 

1. In the **DNS Management** blade, select **+ Virtual network links**.

1. Select **+ Add"** and configure the virtual network link. 

    | Property                 | Value             |
    | :----------------------- | :---------------- |
    | Link name                | `app-vnet-link` |
    | Virtual network          | **app-vnet**      |
    | Enable auto registration | **Enabled**       |

1. Select **Create** and wait for the deployment to finish. If necessary, **Refresh** the page. 

### Create a DNS record set

[DNS records](https://learn.microsoft.com/en-us/azure/dns/dns-zones-records#dns-records) provide information about the DNS zone. 

1. In the portal, continue working on the **private.contoso.com** DNS zone. 

1. In the **DNS Management** blade, select **+ Recordsets**.

1. Notice that two A records have automatically been created for each of the virtual machines. 

1. Select **+ Add** and configure a record set. When finished select **Add**. 
   
    | Property   | Value        |
    | :--------- | :----------- |
    | Name       | `backend`    |
    | Type       | **A**        |
    | TTL        | **1**        |
    | IP address | **10.1.1.5** |

**Note:** This record set implies there is a virtual machine in app-vnet with a private IP address of 10.1.1.5.

### Learn more with online training

+ [Introduction to Azure DNS](https://learn.microsoft.com/training/modules/intro-to-azure-dns/). This module explains what Azure DNS does, how it works, and when you should choose to use Azure DNS as a solution to meet your organization’s needs.
+ [Host your domain on Azure DNS](https://learn.microsoft.com/training/modules/host-domain-azure-dns/). In this module, you learn how to create a DNS zone and DNS records.

### Key takeaways

Congratulations on completing the exercise. Here are the main takeaways:

+ Azure DNS is a cloud service that allows you to host and manage domain name system (DNS) domains, also known as DNS zones. 
+ Azure DNS public zones host domain name zone data for records that you intend to be resolved by any host on the internet.
+ Azure Private DNS zones allow you to configure a private DNS zone namespace for private Azure resources.
+ A DNS zone is a collection of DNS records. DNS records provide information about the domain.
