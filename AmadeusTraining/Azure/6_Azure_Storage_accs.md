# Azure Storage Accounts

storage account provides a unique namespace for your Azure Storage data that's accessible from anywhere in the world over HTTP or HTTPS. Data in this account is secure, highly available, durable, and massively scalable.

Redundancy Options:
- Locally redundant storage (LRS)
- Geo-redundant storage (GRS)
- Read-access geo-redundant storage (RA-GRS)
- Zone-redundant storage (ZRS)
- Geo-zone-redundant storage (GZRS)
- Read-access geo-zone-redundant storage (RA-GZRS)

### storage account endpoints
|Storage service|Endpoint|
|-|-|
|Blob Storage|https://<storage-account-name>.blob.core.windows.net|
|Data Lake Storage Gen2|https://<storage-account-name>.dfs.core.windows.net|
|Azure Files|	https://<storage-account-name>.file.core.windows.net|
|Queue Storage|https://<storage-account-name>.queue.core.windows.net|
|Table Storage|https://<storage-account-name>.table.core.windows.net|

Azure storage always store multiple copies of your data to protect it from un/planned events. Redundancy ensures that your storage account meet its availability and durability targets even in the face of failures.

The factors that help determine which redundancy option you should choose include:
- How your data is replicated in the primary region.
- Whether your data is replicated to a second region that is geographically distant to the primary region, to protect against regional disasters.
- Whether your application requires read access to the replicated data in the secondary region if the primary region becomes unavailable.

## *Locally redundant storage*
*`replicates your data three times`* within a single data center in the primary region. 

LRS provides `99.999999999%` of objects over a given year. The lowest-cost redundancy option and offers the least durability compared to other options.

## *Zone-redundant storage*
replicates your Azure Storage data synchronously *`across three Azure availability zones`* in the primary region. 

ZRS offers durability for Azure Storage data objects of `99.9999999999%` over a given year.

## *Geo-redundant storage*
copies your data synchronously three times within a single physical location in the primary region using LRS. It then copies your data asynchronously to a single physical location in the secondary region (the region pair) using LRS. 

GRS offers durability for Azure Storage data objects of `99.99999999999999%` over a given year.

## *Geo-zone-redundant storage*
Data in a GZRS storage account is copied across three Azure availability zones in the primary region (similar to ZRS) and is also replicated to a secondary geographic region, using LRS, for protection from regional disasters. 

Designed to provide `99.99999999999999%` of durability of objects over a given year.

<br>

# Storage Services

Azure storage platform includes the following data services:
- **Azure Blobs** - massively scalable object store for text and binary data.
- **Azure File** - managed file shares for cloud or on-premise deployments.
- **Azure Queues** - messaging store for reliable messaging between application components.
- **Azure Disks** - block-level storage volumes of VMs.

### **`Blog Storage`** 
is an object storage solution that can store massive amounts of data such as text or binary. It is unstructured so there are no file restrictions. It is ideal for:
- serving images or docs directly to a browser.
- storing files for distributed access.
- streaming video and audio.
- storing data for backup and restore, disaster recovery and archiving
- storing data for analysis by an on-premise or azure-hosted service.

#### Blog storage tiers
- **`Hot Access Tier`** - optimized for storing data that is accessed frequently.
- **`Cool Access Tier`** - optimized for data that is infrequently accessed and stored for at least 30 days.
- **`Archive Access Tier`** - appropriate for data that is rarely accessed and stored for at least 180 days.

## **`Azure Files`**
offers fully managed file shares in the cloud that are accessible via the industry standard Server Message Block (SMB) or Network File System (NFS) protocols. 

## **`Queue storage`**
 a service for storing large numbers of messages. Once stored, you can access the messages from anywhere in the world via authenticated calls using HTTP or HTTPS. 

 ## **`Disk Storage`**
 or Azure managed disks, are block-level storage volumes managed by Azure for use with Azure VMs. Conceptually, they’re the same as a physical disk, but they’re virtualized.