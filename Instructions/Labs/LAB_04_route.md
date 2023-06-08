---
lab:
    title: 'Exercise: Route traffic to the Firewall'
    module: 'Guided Project - Configure secure access to workloads with Azure virtual networking services'
---

# Lab: Route traffic to the Firewall


## Scenario

Now that a firewall is in place with polices that enforce your organizations security requirements, you need to route your network traffic to the firewall subnet so it can filter and inspect the traffic. Route tables provide control over the routing of network traffic to and from the web application. Network Traffic is subject to the firewall rules when you route your network traffic to the firewalll as the subnet default gateway. 

### Architecture diagram


![Diagram that shows one virtual network with a firewall and route table.](../Media/task-3.png)

### Skilling tasks

- Create and configure a route table.
- Link a route table to a subnet.
  

## Exercise instructions

1. Record the private and public IP address of **app-vnet-firewall**.

1. Create a route table named **app-vnet-firewall-rt** in the **RG1** resource group using the East US region.

1. Associate the **app-vnet-firewall-rt** route table to the **frontend** and **backend** subnets in **app-vnet**. 

1. Create a route in the **app-vnet-firewall-rt** named **outbound-firewall** with address prefix **0.0.0.0/0** and **Next hop type**  **Virtual Appliance**. Use the private IP address of the firewall for the **Next hop address**. [Learn more on creating route tables](https://docs.microsoft.com/azure/virtual-network/manage-route-table) and [associating a route table to a subnet](https://docs.microsoft.com/azure/virtual-network/tutorial-create-route-table-portal#associate-a-route-table-to-a-subnet).

Now the outbound traffic from the front end and backend subnet will route to the firewall. 


