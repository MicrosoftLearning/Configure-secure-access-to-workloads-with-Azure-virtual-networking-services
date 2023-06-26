---
demo:
    title: 'Demonstration: Create and configure Azure DNS'
    module: 'Guided Project - Configure secure access to workloads with Azure virtual networking services'
---
## Demonstration – Create and configure Azure DNS

In this demonstration, you will explore Azure DNS.

[Tutorial: Host your domain and subdomain - Azure DNS](https://docs.microsoft.com/azure/dns/dns-delegate-domain-azure-dns)


**Create a private DNS zone**

1. Access the Azure Portal.

1. Search for the **DNS zones** service.

1. Create a **DNS zone** and explain the purpose of the zone. For a name you can use contoso.internal.com.

1.  Wait for the DNS zone to be created. You may need to **Refresh** the page.

**Add a DNS record set**


[Tutorial: Create an alias record to refer to a zone resource record](https://learn.microsoft.com/azure/dns/tutorial-alias-rr)

1. Once your zone is created, select **+Record Set**.

1. Use the **Type** drop-down to view the different types of records. Review how the different record types are used. Notice how the record information changes as you select different record types.

1. Create an **A** record as an example. 

**Link VNet for auto registration**

1.	Once the DNS Zone is deployed review the overview page with the students.
1.	link the private DNS zone to a virtual network, by creating a virtual network link.
1.	On the left pane, select Virtual network links.
1.	Select Add.
1.	Type myLink for the Link name.
1.	For Virtual network, select myAzureVNet.
1.	Select the Enable auto registration check box.
1.	Select OK.

>**Note**: Students should now be able to complete LAB_05