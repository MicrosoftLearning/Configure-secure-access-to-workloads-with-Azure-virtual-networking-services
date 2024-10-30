---
demo:
    title: 'Demonstration: Create and configure network routing'
    module: 'Guided Project - Configure secure access to workloads with Azure virtual networking services'
---
## Demonstration – Create and configure network routing

In this demonstration, we will learn how to create a route table, define
a custom route, and associate the route with a subnet. 


**Note:** This demonstration requires a virtual network with at least one subnet.

[Route network traffic - tutorial - Azure portal](https://learn.microsoft.com/azure/virtual-network/tutorial-create-route-table-portal#create-a-route-table)


### Create a Route table 

1. As you have time review the tutorial diagram. Explain why you need to create a user-defined route. 

1. Access the Azure portal.

1. Search for and select **Route tables**. Discuss when **propagate gateway routes** should be used. 

1. Create a routing table, explain any uncommon settings. 

1. Wait for the new routing table to be deployed.

**Add a route**

1.  Select your new routing table, and then select **Routes**.

1.  Create a new **route**. Discuss the different **hop types** that are available. 

1.  Create the new route and wait for the resource to be deployed.
 
### Associate a Route Table to a subnet
A route table can be associated to zero or more subnets. Route tables aren't associated to virtual networks. You must associate a route table to each subnet you want the route table associated to.


1.  Navigate to the subnet you want to associate with the routing table.

1.  Select **Route table** and choose your new routing table. 

1.  **Save** your changes.

 
>**Note**: You can only associate a route table to subnets in virtual networks that exist in the same Azure location and subscription as the route table.

>**Note**: Students should now be able to complete LAB_04
