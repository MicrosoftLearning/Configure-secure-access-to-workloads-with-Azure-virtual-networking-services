---
demo:
    title: 'Demonstration: Create and configure Azure DNS'
    module: 'Guided Project - Configure secure access to workloads with Azure virtual networking services'
---
## Demonstration – Create and configure Azure DNS

In this demonstration, we will explore Azure DNS by creating a DNS zone, an A record, and enabling auto registration for a virtual network. 
[slide]
1.	On the portal search bar, type private dns zones in the search text box and press Enter.
2.	Select Private DNS zone.
3.	Select Create private dns zone.
4.	On the Create Private DNS zone page, type or select the following values:
o	Resource group: Select existing. 
o	Name: Type private.contoso.com for this example.
5.	For Resource group location, select West Central US.
6.	Select Review + Create.
7.	Select Create.
8.	Once the DNS Zone is deployed review the overview page with the students.
9.	link the private DNS zone to a virtual network, by creating a virtual network link.
10.	On the left pane, select Virtual network links.
11.	Select Add.
12.	Type myLink for the Link name.
13.	For Virtual network, select myAzureVNet.
14.	Select the Enable auto registration check box.
15.	Select OK.

>**Note**: Students should now be able to complete LAB_05