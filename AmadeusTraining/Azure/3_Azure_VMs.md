# Azure Virtual Machines

You can create and use VMs in the cloud. They provide IaaS in the form of virtualized server and can be used in many ways.

You can customize all of the software running on your VM. It's ideal when you need:
- Total control over the OS
- ability to run custom software
- use custom hosting configurations

However, being IaaS offering, you still need to configure, update, and maintain the software.

## Scaling with VMs

You can run single VMs for testing, developement or minor tasks. Or you can group VMs together to provide high availability, scalability, and redundancy. 

## **`VM Scale Sets`**
if you simply create multiple VMs with the same purpose, you would need to:
- ensure they were all configured identically
- set up network routing parameters to ensure efficiency 
- monitor the utilization to determine if you need to increase or decrease the number of VMs. 

Azure **`VM scale sets`** automatically does most of that work. It allows you to centrally manage, configure, and update a large number of VMs in minutes.

- The number of VM instances can automatically increase or decrease in response to demand
- settable to scale based on a defined schedule
- automatically deploy a load balancer to make sure that your resources are being used efficiently
- build large-scale services for areas such as compute, big data, and container workloads.

## **`VM Availability Sets`**

designed to ensure that VMs stagger updates have varied power and network connectivity, preventing you from losing all your VMs with a single network or power failure.

Availability sets do this by grouping VMs in two ways:
- **`Update domain`** - groups VMs that can be rebooted at the same time. Allows you to apply updates while knowing that only one update domain grouping will be offline at a time. 
    > an update group going through the update process is given a 30-minute time to recover before maintenance on the next update domain starts.
- **`Fault domain`** - groups VMs by common power source and network switch. By default, splits your VMs across up to 3 fault domains which helps protect against physical power or networking failure.

## When to use VMs
- **During Testing and development**
- **When running applications in the cloud** as opposed to creating traditional infrastructure. You can shut down VMs when needed or quickly starting them to meet a sudden demand increase. 
- **When extending your datacenter to the cloud**. an organization with its own on-premise network can create Virtual network in Azure and adding VMs to that virtual network.
- **During disaster recovery** - if a primary datacenter fails, you can create VMs running on azure to run your critical applications.

When you provision a VM, you can pick the resources that are associated such as:
- Size (processor cores, RAM)
- Storage 
- Networking (virtual network, public IP, port configurations)
