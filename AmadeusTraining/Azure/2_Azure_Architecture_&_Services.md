# Azure architecture and services

Azure provides more than 100 services that lets you do everything from running your existing apps on VMs to exploring new software paradigms.

### Getting Started

You need an Azure subscription which needs an Azure account. Afterwards, you can start creating Azure resources within each subscription.

![a](.imgs/Azure-accounts.png)

---

## Physical infrastructure
As a global cloud provider, Azure has datacenters around the world. These are grouped into Azure Regions or Availability Zones.

**Regions** is a geographical area on the planet that contains at least one datacenter that are nearby and networked together with low-latency network.

When you deploy a resource in Azure, you'll often need to choose the region where you want your resource deployed.

> Note: Some services or VM features are only available in certain regions such as specific VM size or storage types. 

**Availability Zones** are physically separate datacenters within an Azure region. EAch zone is made up of one or more datacenters equipped with independent power, cooling and networking. These zones are set up to be an isolation boundary. If one goes down, the other continues working. 

![](.imgs/Azure-Regions.png)

To ensure your services and data are redundant so you can protect your information in case of failure. 

You can use availability zones to run mission-critical applications and build high-availability into your application architecture by co-locating your compute, storage, networking, and data resources within an availability zone and replicating in other availability zones.

**Availability zones** are primarily for VMs, managed disks, load balancers, and SQL databases. Azure services that support availability zones fall into three categories:
- **Zonal services** 
    - You pin the resource to a specific zone
    - e.g. VMs, managed disks, IP addresses.
- **Zone-redundant services**
    - the platform replicates automatically across zones
    - zone-redundant storage, SQL Database
- **Non-regional services**
    - services are always available from azure geographies and are resilient to zone-wide outages as well as region-wide outages.

But even with additional resiliency that availability zones provide, it's still possible for an event to be so large it impacts multiple availability zones in a single region. Hence why Region pairs exists.

**Region pairs** are paired with another region within the same geography at least 300 miles away. 

![](.imgs/Azure-Region-Pairs.png)