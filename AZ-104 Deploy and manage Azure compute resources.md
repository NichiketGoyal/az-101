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


