# openshift-virt-vm-automation
Automation to manage virtual machines in OpenShift

## Overview

The contents of this repository demonstrates how to manage a virtual machine lifecycle (provision/deprovision/patching/snapshot/recovery) through automation.

### Golden Image Creation
![High Level Architecture](/images/golden-image-creation-hld-flow-dev-hub-01.drawio.png)<br/>

1. User requests for creation of golden image in a self service model using API
2. API triggers associated CI pipeline 
3. CI pipeline executes series of tasks as shown in diagram
   - Validating input parameters received from API 
   - Create data volume from openshift-virtualization-os-images or
   - Import disk image from Red Hat CDN 
   - Create necessary secrets such as root password, Red Hat Subcription account password, Public SSH key
   - Customize image such as  
     - Change root password
     - Subcribe to Red Hat 
     - Install packages 
     - Run SE Linux re-labelling 
     - Upload configuration files etc 
5. Push golden image to image repository 
4. Provide feedback to user 

### Virtual Machine Provisioning

An overview of the architecture can be found below:
![High Level Architecture](/images/vm-provision-hld-flow-dev-hub-01.drawio.png)<br/>

1. User requests for creation virtual machine using predefined templates in a self service model using API
2. API triggers associated CI pipeline 
3. CI pipeline executes series of tasks as shown in diagram
5. Creates required artifacts and performs push activity to Git
4. Kubernetes reconciler identifies new changes and applies artifacts to create a VM

[ACM Placement API](https://open-cluster-management.io/docs/concepts/content-placement/placement/)<br/>
[ACM Placement API Integration with ArgoCD](https://open-cluster-management.io/docs/scenarios/integration-with-argocd/)


### Virtual Machine De-provisioning
![High Level Architecture](/images/vm-deprovision-hld-flow-dev-hub-01.drawio.png)<br/>

1. User requests for deprovisin/deletion of a virtual machine in a self service model using API
2. API triggers associated CI pipeline 
3. CI pipeline executes series of tasks as shown in diagram
5. Creates required artifacts and performs push activity to Git
4. Kubernetes reconciler identifies new changes and applies artifacts to delete a VM

### Virtual Machine Rebuild/Repave
![High Level Architecture](/images/vm-repave-hld-flow-dev-hub-01.drawio.png) <br/>

1. User requests for repave/rebuild of a virtual machine in a self service model using API
2. API triggers associated CI pipeline 
3. CI pipeline executes series of tasks as shown in diagram 
5. Creates required artifacts and performs push activity to Git
4. Kubernetes reconciler identifies new changes and applies artifacts to spin up a VM with new disk image

### Virtual Machine Patching

![High Level Architecture](/images/vm-patching-hld-flow-dev-hub-01.drawio.png)

1. User requests for apply patch to a virtual machine in a self service model using API
2. API triggers associated CI pipeline 
3. CI pipeline executes series of tasks as shown in diagram 
5. Creates required artifacts and performs push activity to Git
4. Kubernetes reconciler identifies new changes such a stop of a VM and start of a VM and applies them

