# Azure Virtual Machines

You can create and use VMs in the cloud. They provide IaaS in the form of virtualized server and can be used in many ways.

You can customize all of the software running on your VM. It's ideal when you need:
- Total control over the OS
- ability to run custom software
- use custom hosting configurations

However, being IaaS offering, you still need to configure, update, and maintain the software.

## Scaling with VMs

You can run single VMs for testing, developement or minor tasks. Or you can group VMs together to provide high availability, scalability, and redundancy. 

### **`VM scale sets`**
if you simply create multiple VMs with the same purpose, you would need to:
- ensure they were all configured identically
- set up network routing parameters to ensure efficiency 
- monitor the utilization to determine if you need to increase or decrease the number of VMs. 

Azure **`VM scale sets`** automatically does most of that work. It allows you to centrally manage, configure, and update a large number of VMs in minutes.