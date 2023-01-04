# `Azure Functions`
is an event-driven, serverless compute option that doesn't require maintaining VMs or containers. 

**Serverless Computing** - there are servers being used but the responsibility of managing servers is already handled for you. It's an abstraction of servers so you can ignore infrastructure concerns and focus on developer concerns.

3 big benifits:
- no infrastructure management
- scalability - your application can continue working under any workload
- only pay for what you use. resources are only allocated for a direct action.

# `Azure App Service`

enabled you to build and host web apps, background jobs, mobile back-ends and RESTful APIs without managing infrastructure. 

It is an HTTP-based service for hosting web apps, REST APIs, and mobile backends. Supports multiple languages such as .NET/Core, Java, Ruby, Node.js, PHP, or Python.

Common App services supported
- web apps
- API apps
- WebJobs
- Mobile apps

Handles most of the infrastructure decisions:
- deployment and management are integrated into the platform
- endpoints can be secured
- sites can be scaled quickly to handle high traffic loads
- built-in load balancing and traffic manager provide high availability

# `Azure Virtual Networking`
enable Azure resources to communicate with each other, with users on the internet, or with your on-premise client. 

Provides the following networking capabilities:
- isolation and segmentation
- internet communications
- communicate between azure resources
- communicate with on-premise resources
- route network traffic
- filter network traffic
- connect virtual networks

# `Azure Virtual Private Networks`
uses an encrypted tunnel within another network. Typically deployed to connect two or more trusted private networks to one another over an untrusted network (typically the public internet). Traffic is encrypted while travelling over the untrusted network to prevent attacks.

**VPN gateways** are deployed in a dedicated subnet of the virtual network and enable the following connectivity:
- connect on-premise datacenters to virtual networks through a site-to-site connection.
- connect individual devices to virtual networks through a point-to-site connection
- connect virtual networks to other virutal networks through a network-to-network connection

There are ways to maximize the resiliency of your VPN gateway:
- **Active/standby** - by default, gateways are deployed as two instances in an active/standby configuration. When planned maintenance/unplanned disruption affects the active instance, the standby instance assumes responsibility for connections without any user intervention. 
- **Active/active** - In this configuration, you assign a unique public IP address to each instance. You then create separate tunnels from the on-premises device to each IP address.
- **ExpressRoute failover** - 
- **Zone-redundant gateways** - In regions that support availability zones, VPN gateways and ExpressRoute gateways can be deployed in a zone-redundant configuration.


# `Azure ExpressRoute`

lets you extend your on-premises networks into the Microsoft cloud over a private connection, with the help of a connectivity provider called the  *`ExpressRoute Circuit`*.

Supports 4 models that you can use to connect your on-premise network to Microsoft cloud:
- CloudExchange colocation
- Point-to-point ethernet connection
- Any-to-any connection
- Directly from ExpressRoute sites

# `Azure DNS`
a hosting service for DNS domains that provides name resolution by using Microsoft Azure infrastructure. By hosting your domains in Azure, you can manage your DNS records using the same credentials, APIs, tools, and billing as your other Azure services.