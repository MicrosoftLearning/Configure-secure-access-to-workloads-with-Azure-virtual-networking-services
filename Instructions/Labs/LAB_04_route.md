---
lab:
    title: 'Exercise: Route traffic to the Firewall'
    module: 'Guided Project - Configure secure access to workloads with Azure virtual networking services'
---

# Lab: Route traffic to the Firewall

## Scenario

Now that a firewall is in place with policies that enforce your organizations security requirements, you need to route your network traffic to the firewall subnet so it can filter and inspect the traffic. Route tables provide control over the routing of network traffic to and from the web application. Network Traffic is subject to the firewall rules when you route your network traffic to the firewall as the subnet default gateway.

### Architecture diagram

![Diagram that shows one virtual network with a firewall and route table.](../Media/task-3.png)

### Skilling tasks

- Create and configure a route table.
- Link a route table to a subnet.
  
## Exercise instructions

### Create a route table

Azure automatically creates a [route table](https://learn.microsoft.com/azure/virtual-network/virtual-networks-udr-overview) for each subnet within an Azure virtual network. The route table includes the default [system  routes](https://learn.microsoft.com/azure/virtual-network/virtual-networks-udr-overview#system-routes). You can create route tables and routes to override Azure's default system routes.

1. Record the private and public IP address of **app-vnet-firewall**.

    1. In the search box at the top of the portal, enter **Firewall**. Select **Firewall** in the search results.

    1. Select **app-vnet-firewall**.

    1. Select **Overview**.

        1. Record the **Private IP address**.

    1. In the Overview pane select on **fwpip**

    1. Record the **Public IP address**.

1. In the search box, enter **Route tables**. When Route table appears in the search results, select it.

1. In the Route table page, select **+ Create**.

1. On the **Basics** tab of Create Route table, enter the information as listed in the table below:

    | Property       | Value                        |
    | :------------- | :--------------------------- |
    | Subscription   | **Select your subscription** |
    | Resource group | **RG1**                      |
    | Region         | **East US**                  |
    | Name           | **app-vnet-firewall-rt**     |

1. Select **Review + create** and then select **Create**.

### Associate the route table to the subnets

1. In the search box, enter **Route tables**. and select Route Tables from the search results.

1. Select **app-vnet-firewall-rt**.

1. Select **Subnets**.

1. Select **+ Associate**.

1. On the **Associate subnet** page, enter the information as listed in the table below:

    | Property        | Value              |
    | :-------------- | :----------------- |
    | Virtual network | **app-vnet (RG1)** |
    | Subnet          | **frontend**       |

1. Select **OK**.

1. Repeat the steps above to associate the **app-vnet-firewall-rt** route table to the **backend** subnet in **app-vnet**.

### Create a route in the route table

1. In the search box, enter **Route tables**. and select Route Tables from the search results.

1. Select **app-vnet-firewall-rt**.

1. Select **Routes**.

1. Select **+ Add**.

1. On the **Add route** page, enter the information as listed in the table below:

    | Property                            | Value                                                   |
    | :---------------------------------- | :------------------------------------------------------ |
    | Route name                          | **outbound-firewall**                                   |
    | Destination type                    | **IP addresses**                                        |
    | Destination IP addresses/CIDR range | **0.0.0.0/0**                                           |
    | Next hop type                       | **Virtual appliance**                                   |
    | Next hop address                    | **private IP address of the firewall recorded earlier** |

1. Select **Add**.

### Learn more with online training

+ [Manage and control traffic flow in your Azure deployment with routes](https://learn.microsoft.com/training/modules/control-network-traffic-flow-with-routes/). In this module, you learn how to control Azure virtual network traffic by implementing custom routes. This module has two sandboxes. 

### Key takeaways

Congratulations on completing the exercise. Here are the main takeaways:

+ Network traffic in Azure is automatically routed across Azure subnets, virtual networks, and on-premises networks. System routes control this routing.
+ User-defined routes override the default system routes so traffic can be routed through a network virtual appliances (NVAs). 
+ Network virtual appliances (NVAs) control the flow of network traffic. Examples of NVAs are firewalls, load balancers, and routers.
+ Route tables contain routing information and are associated with a subnet. 
