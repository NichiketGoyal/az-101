# 1. Configure Virtual Machines

### Things to know about Azure Virtual Machines:
- Azure Virtual Machines is the basis of the Azure infrastructure as a service (IaaS) mode
- provides its own operating system, storage, and networking capabilities
- can implement multiple virtual machines, and configure each machine with different software and settings
- virtual machines can quickly scale up and down with demand and pay only for what you use.
- The responsibilities associated with configuring and maintaining virtual machines is shared between Microsoft and the customer.

### Scenarios for working with IaaS and virtual machines:
- Easier to set up test and development environments.
- Website hosting is cheaper.
- Easier storage, backup, and recovery without complexity of storage management.
- Enables high-performance computing, helpful in solving complex problems. 
- Helps in big data analysis . 
- Add extended datacenters by adding VM in azure with a click. 

### Virtual Machine Pricing:
- ***Compute expenses*** are priced on a per-hour basis but billed on a per-minute basis
  - **Consumption-based:** Increase and Decrease capacity on demand. Pay for comute capacity by second
  - **Reserved Virtual Machine Instances:** advance purchase of a virtual machine for one or three years in a specified region. Get up to 72% price savings compared to pay-as-you-go pricing
- ***Storage costs*** are charged separately for the Azure Storage used by the virtual machine.

### Virtual Machine Location:
- Each region has different hardware available, and some configurations aren't available in all regions.
- There are price differences between locations.

### Virtual Machine Size:
- Azure provides a wide range of virtual machine size options with mix of compute, memory, and storage for your needs.
- You can resize a virtual machine anytime if your current hardware configuration is allowed in the new size.

### Virtual Machine Storage:
Virtual Machine has 3 disks attached to itself. Operating System Disk, Temporary Disk, Data Disk.
- **Azure Premium Storage**: high-performance, low-latency disk, uses SSD
- **Multiple Storage Disks:** attach several Premium Storage disks to a virtual machine upto 256 TB per VM
- **Managed Disks:** stored as page blobs, which are a random IO storage object in Azure. Azure creates and manages the disk for you. Can be SSD or HDD.

### Connect to VM's:
- **Windows**: use the Microsoft Remote Desktop application with the remote desktop protocol (RDP). It provides Graphical User Interface(GUI). 
- **Linux**: use a secure shell protocol (SSH) client. public key is placed on your Linux virtual machine, private key remains on your local system.
- **Azure Bastion** service is a fully platform-managed PaaS service. Azure Bastion provides secure and seamless RDP/SSH connectivity to your virtual machines directly over SSL


# 2. Configure Virtual Machines Availability

### Availability Sets
An availability set is a logical feature you can use to ensure a group of related virtual machines are deployed together.
#### Characteristics:
- All virtual machines in an availability set should perform the identical set of functionalities.
- All virtual machines in an availability set should have the same software installed.
- All VM's run across multiple physical servers, compute racks, storage units, and network switches.
- A virtual machine can only be added to an availability set when the virtual machine is created.
#### Why to use Availability Sets
- To achieve redundancy in your configuration
- Each application tier exercised in your configuration should be located in a separate availability set. The separation helps to mitigate single point of failure on all machines.
- For high availability and network performance, create a load-balanced availability set by using Azure Load Balancer.
- You can use Azure managed disks with your Azure virtual machines in availability sets for block-level storage.

### Update Domain
- An update domain is a group of nodes that are upgraded together during the process of a service upgrade (or rollout).
- During planned maintenance, only one update domain is rebooted at a time.
- By default, there are five (non-user-configurable) update domains. You can configure upto 20

### Fault Domain
- A fault domain is a group of nodes that represent a physical unit of failure.
- Two fault domains work together to mitigate against hardware failures, network outages, power interruptions, or software updates.

<img width="581" alt="Screenshot 2023-01-02 at 6 44 26 PM" src="https://user-images.githubusercontent.com/47356500/210236264-30caf604-9ae7-441d-bf8f-682077e8ed2f.png">


### Availability Zones
- Availability zones are a high-availability offering that protects your applications and data from datacenter failures.
- Combination of a fault domain and an update domain makes an availability zone.
- These are equipped with independent power, cooling, and networking.
- To ensure resiliency, there's a minimum of three separate zones in all enabled regions.
- The physical separation of availability zones within a region protects applications and data from datacenter failures.

### Vertical Scaling
It involves increasing or decreasing the virtual machine size in response to a workload. Vertical scaling makes a virtual machine more (scale up) or less (scale down) powerful.

### Horizontal Scaling
It is used to adjust the number of virtual machines in your configuration to support the changing workload.

####Things to consider Using Vertical and Horizontal Scaling:
- **Horizontal scaling has fewer limitations than vertical scaling**: 
  - Vertical scaling also usually requires a virtual machine to stop and restart
  - A vertical scaling implementation depends on the availability of larger hardware
- When operating in the cloud, horizontal scaling is more flexible

### Azure Virtual Machine Scale Sets
- Azure Virtual Machine Scale Sets are an Azure Compute resource that you can use to deploy and manage a set of identical virtual machines.
- It is used to gain true **Auto-Scaling**
- All virtual machine instances are created from the same base operating system image and configuration.
- You can use Virtual Machine Scale Sets to run multiple instances of your application.
- Virtual Machine Scale Sets support up to 1,000 virtual machine instances.

#### Things to consider
- create autoscaling rules to define the acceptable performance
- If the increased load is consistent, rather than a brief demand, you can configure autoscale rules to increase or decrease the number of virtual machine instances in your implementation.
- schedule events to automatically increase or decrease the capacity of your implementation
- reduces your management overhead to monitor and optimize the performance


# 3. Configure Virtual Machines Extensions

### Virtual Machines Extensions
Azure virtual machine extensions are small applications that provide post-deployment configuration and automation tasks for Azure Virtual Machines.
Example software installation or anti-virus protection, or when a machine needs to run a configuration script.

#### Characteristics:
- Can be managed via Azure CLI, PowerShell, Azure Resource Manager (ARM) templates, and the Azure portal.
- can be bundled with a new virtual machine deployment or run against any existing system.
- can choose from a large set of first and third-party virtual machine extensions.

#### Ways to Implement:
- can be a subset of a larger deployment for your virtual machines.
- can be used as configuration applications to assist with provisioning your virtual machines.
- can be run against any supported extension operated systems after deployment.

### Custom Script Extensions
- used to automatically launch and execute virtual machine customization tasks after initial machine configuration.
- After the Custom Script Extensions resource is created for your virtual machine, you provide a PowerShell script file with the commands to execute on the machine.
- Scripts can be downloaded from Azure Storage or GitHub, or provided to the Azure portal at extension run time.
- Timeout time is 90 mins

### Desired State Configuration
Desired State Configuration is a management platform in Windows PowerShell. Desired State Configuration enables deploying and managing configuration data for software services and managing the environment in which these services run.
- Desired State Configuration centers around creating specific configurations by using scripts.


# 4. Configure Azure app service plans

### Things to know:
- An App Service plan defines a set of compute resources for a web application to run.
- Each App Service plan defines three settings:
  - Region: The region for the App Service plan, such as West US, Central India, North Europe, and so on.
  - Number of VM instances: The number of virtual machine instances to allocate for the plan.
  - Size of VM instances: The size of the virtual machine instances in the plan, including Small, Medium, or Large.
- You can add new apps to existing plan.

### How applications run and scale in App Service plans
The Azure App Service plan is the scale unit of App Service applications. 
- Free or Shared tier:
  - Applications run by receiving CPU minutes on a shared virtual machine instance.
  - Applications can't scale out.
- Basic, Standard, Premium, or Isolated tier:
  - Applications run on all virtual machine instances configured in the App Service plan.
  - Multiple applications in the same plan share the same virtual machine instances.
  - If you have multiple deployment slots for an application, all deployment slots run on the same virtual machine instances.
  - If you enable diagnostic logs, perform backups, or run WebJobs, these tasks use CPU cycles and memory on the same virtual machine instances.

### Things to consider
- **cost savings** as you pay for the computing resources that your App Service plan allocates.
- **multiple applications in one plan** a single plan to support multiple applications, to make it easier to configure and maintain shared virtual machine instances.
- **plan capacity** determine the resource requirements for the new application and identify the remaining capacity of your plan.
- **application isolation** need to scale the application independently from the other applications in the existing plan, or in a different region or app is resource-intensive. 

### Pricing
<img width="915" alt="Screenshot 2023-01-03 at 2 31 37 PM" src="https://user-images.githubusercontent.com/47356500/210326658-6c348cdd-085d-4423-ad5e-bc95882a1f0c.png">

### Azure App Service scaling
- Both horizontal and vertical scaling is available.
- You can scale out to as many as 30 instances, depending on your App Service plan pricing tier
- Changing your scale settings, you don't need to change your code or redeploy your applications.
- autoscale to support users and reduce costs

### Azure App Service auto-scaling
- need to specify the minimum, and maximum number of instances to run
- An autoscale setting is read by the autoscale engine to determine whether to scale out or in.
- Autoscale trigger can be metric-based or time-based
- The autoscale engine uses notification settings.

