---
demo:
    title: 'Demonstration: Create and configure Azure Firewall'
    module: 'Guided Project - Configure secure access to workloads with Azure virtual networking services'
---
## Demonstration – Create and configure Azure Firewall

**Note:** Azure Firewall can take a few minutes to deploy.

In this demonstration, explore Azure Firewall.
Review and create an Azure Firewall and Firewall policy.
1.	[Supporting Slide] Before beginning the demonstration, let's review what Azure Firewall is.
2.	Access the Azure portal.
3.	Create an Azure Firewall.
4.	ⓘ on the Basics tab explain the configuration options available as you fill them out. 
5.	Accept the other default values, then select Review + create.
6.	After deployment is completed, go to the firewall resource, and review the overview page. 


### Configure an application rule 

1. [Supporting Slide] Azure Firewall policy rules

This is the application rule that allows outbound access to www.google.com.
1.	Navigate to the firewall policy you created.
2.	Select Application rules.
3.	Select Add a rule collection.
4.	For Name, enter App-Coll01.
5.	For Priority, enter 200.
6.	For Rule collection action, select Allow.
7.	Under Rules, for Name, enter Allow-Google.
8.	For Source type, select IP address.
9.	For Source, enter 10.0.2.0/24.
10.	For Protocol:port, enter http, https.
11.	For Destination Type, select FQDN.
12.	For Destination, enter www.google.com
13.	Select Add.

Azure Firewall includes a built-in rule collection for infrastructure FQDNs that are allowed by default. These FQDNs are specific for the platform and can't be used for other purposes. For more information, see Infrastructure FQDNs.

### Configure a network rule
This is the network rule that allows outbound access to two IP addresses at port 53 (DNS).
1.	Select Network rules.
2.	Select Add a rule collection.
3.	For Name, enter Net-Coll01.
4.	For Priority, enter 200.
5.	For Rule collection action, select Allow.
6.	For Rule collection group, select DefaultNetworkRuleCollectionGroup.
7.	Under Rules, for Name, enter Allow-DNS.
8.	For Source type, select IP Address.
9.	For Source, enter 10.0.2.0/24.
10.	For Protocol, select UDP.
11.	For Destination Ports, enter 53.
12.	For Destination type select IP address.

>**Note**: Students should now be able to complete LAB_04
14.	For Destination, enter 209.244.0.3, 209.244.0.4.
These are public DNS servers operated by CenturyLink.
15.	Select Add.

