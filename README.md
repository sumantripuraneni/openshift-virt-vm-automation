# openshift-virt-vm-automation
Automation to manage virtual machines in OpenShift

## Overview

The contents of this repository demonstrates how to manage a virtual machine lifecycle (provision/deprovision/patching/snapshot/recovery) through automation.

### Virtual Machine Provisioning

An overview of the architecture can be found below:
![High Level Architecture](/images/vm-provision-hld-flow-dev-hub.drawio.png)
1. User requests a virtual machine in a self service model using API/GUI (Catalog from OpenSHift Developer Hub)
2. Developer Hub triggers associated tekton pipeline 
3. Tekton pipeline executes imperative tasks (examples below), prepares VM definitio and pushes to Git
4. ACM creates a VM on a managed cluster by using `Prioritizers`
[ACM Placement Decision](https://open-cluster-management.io/docs/concepts/content-placement/placement/)

#### Imperative Task Examples:
1. API call to IPAM 
2. Virtual Machine name generation 
3. DNS registration
4. Customizing image
   - Configure Red Hat subscription 
   - Root password generation 
   - Store root password in CMDB
   - Package installation 
   - SSH key generation 
   - Enable systemctl services (application specific)
5. Template out virtual machine definition and push to git repository 


#### Building/Customizing Virtual Machine images
1. [Cloud-init](https://cloud-init.io/): Cloud-init is a method for cross-platform cloud instance initialization. It is supported across all major public cloud providers, private cloud infrastructure, and bare-metal installations.
2. [Virt-customize](https://libguestfs.org/virt-customize.1.html): Virt-customize can customize a virtual machine (disk image) by installing packages, editing configuration files, and so on
3. [Packer](https://github.com/hashicorp/packer): Packer is another tool for creating identical Virtual Machine (VM) images for multiple platforms from a single source configuration.

### Virtual Machine De-provisioning
![High Level Architecture](/images/vm-deprovision-hld-flow-dev-hub.drawio.png)

### Virtual Machine Rebuild/Repave
![High Level Architecture](/images/vm-repave-hld-flow-dev-hub.drawio.png)

### Virtual Machine Patching

![High Level Architecture](/images/vm-patching-hld-flow-dev-hub.drawio.png)