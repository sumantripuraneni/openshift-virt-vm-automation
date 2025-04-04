# openshift-virt-vm-automation
Automation to manage virtual machines in OpenShift

## Overview

The contents of this repository demonstrates how to manage a virtual machine lifecycle (provision/deprovision/patching/snapshot/recovery) through automation.

### Virtual Machine Provisioning

An overview of the architecture can be found below:
![High Level Architecture](/images/vm-provision-hld-flow-dev-hub-01.drawio.png)
1. User requests a virtual machine in a self service model using API
2. API triggers associated CI pipeline 
3. CO pipeline executes series of tasks as shown in diagram
5. Push created artifacts to Git
4. Kubernetes reconciler identifies new changes and applies (creates virtual machine)

[ACM Placement Decision](https://open-cluster-management.io/docs/concepts/content-placement/placement/)<br/>
[Placement API Integration with Argo CD](https://open-cluster-management.io/docs/scenarios/integration-with-argocd/)


### Virtual Machine De-provisioning
![High Level Architecture](/images/vm-deprovision-hld-flow-dev-hub.drawio.png)

### Virtual Machine Rebuild/Repave
![High Level Architecture](/images/vm-repave-hld-flow-dev-hub.drawio.png)

### Virtual Machine Patching

![High Level Architecture](/images/vm-patching-hld-flow-dev-hub.drawio.png)



