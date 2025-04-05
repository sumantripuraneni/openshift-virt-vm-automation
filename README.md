# openshift-virt-vm-automation
Automation to manage virtual machines in OpenShift

## Overview

The contents of this repository demonstrates how to manage a virtual machine lifecycle (provision/deprovision/patching/snapshot/recovery) through automation.

### Virtual Machine Provisioning

An overview of the architecture can be found below:
![High Level Architecture](/images/vm-provision-hld-flow-dev-hub-01.drawio.png)
1. User requests for creation virtual machine using predefined templates in a self service model using API
2. API triggers associated CI pipeline 
3. CI pipeline executes series of tasks as shown in diagram
5. Created required artifacts and performs push activity to Git
4. Kubernetes reconciler identifies new changes and applies artiafcts to create a VM

[ACM Placement API](https://open-cluster-management.io/docs/concepts/content-placement/placement/)<br/>
[ACM Placement API Integration with ArgoCD](https://open-cluster-management.io/docs/scenarios/integration-with-argocd/)


### Virtual Machine De-provisioning
![High Level Architecture](/images/vm-deprovision-hld-flow-dev-hub-01.drawio.png)

### Virtual Machine Rebuild/Repave
![High Level Architecture](/images/vm-repave-hld-flow-dev-hub-01.drawio.png)

### Virtual Machine Patching

![High Level Architecture](/images/vm-patching-hld-flow-dev-hub.drawio.png)



