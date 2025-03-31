# openshift-virt-vm-automation
Automation to manage virtual machines in OpenShift

## Overview

The contents of this repository demonstrates how to manage a virtual machine lifecycle (provision/deprovision/patching/snapshot/recovery) through automation.

### VM Provisioning

An overview of the architecture can be found below:
![High Level Architecture](/images/vm-provision-hld-flow-dev-hub.drawio.png)

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