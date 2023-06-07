---
demo:
    title: 'Demonstration: Create and configure network routing'
    module: 'Guided Project - Configure secure access to workloads with Azure virtual networking services'
---
## Demonstration – Create and configure network routing

In this demonstration, we will explore network routing and Azure Route tables. 

### Create a Route table. 
1.	In the Route table page, select Create.
2.	In the Create route table enter the route table name and explain the Propagate gateway routes setting. 
3.	View details of thew route table you created. 
Create a Route
1.	From the route table menu bar, choose Routes and then select + Add.
2.	Enter a unique Route name for the route within the route table.
 
### Associate a Route Table to a subnet
A route table can be associated to zero or more subnets. Route tables aren't associated to virtual networks. You must associate a route table to each subnet you want the route table associated to.

Azure routes all traffic leaving the subnet based on routes you've created:
•	Within route tables
•	Default routes
•	Routes propagated from an on-premises network if the virtual network is connected to an Azure virtual network gateway (ExpressRoute or VPN).

>**Note**: You can only associate a route table to subnets in virtual networks that exist in the same Azure location and subscription as the route table.

>**Note**: Students should now be able to complete LAB_04