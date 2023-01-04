# Azure Virtual Desktop

is a desktop and application virtualization service that runs on the cloud. It enables you to use the cloud-hosted version of Windows from any location. 

## Azure containers
VMs are still limited to a single operating system per machine. If you want to run multiple instances of an application on a single host machine, **containers** are an excellent choice.

**`Containers`** are virtualization environment. Like running multiple VMs on a physical host, you can run multiple containers on a single physical or virtual host. One of thoe most popular container engine is *`Docker`* which is supported by Azure

**`Containers`** bundle a single app and its dependencies (referred to as containerizing the app) then deploys it as a unit to a container host. Which provides a standardized run time environment.

|Virtual Machine|Container|
|-|-|
|Virtualize the hardware|virtualze the operating system|
||more lightweight|
||can run multiple containers on a single host|

Azure container instances are PaaS offering. Allows you to upload your containers and then the service will run them for you.

