---
layout: default
title: Fence Agents Remediation
nav_order: 3
has_children: true
parent: Remediation
---

## Fence Agents Remediation

Generally Available
{: .label .label-green }

[Fence Agents Remediation](https://github.com/medik8s/fence-agents-remediation#readme) (FAR) is a Kubernetes operator that uses external tools to remediate unhealthy nodes. The tools are a set of well-known [upstream fence agents (FA)](https://github.com/ClusterLabs/fence-agents), where each one of them can be used for different environments, to fence a node using a reboot action. Moreover, FAR can be used by the [Node HealthCheck Operator](https://github.com/medik8s/node-healthcheck-operator#readme) (or any other operator that supports the external remediation API) as an external remediator.

FAR is recommended when a node becomes unhealthy, and we want to completely isolate the node from a cluster, since we can’t “trust” the unhealthy node, to prevent it from accessing the shared resources like [RWO volumes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#access-modes). The operator is available in the Kuberenets community, [OperatorHub.io](https://operatorhub.io/operator/fence-agents-remediation), and can be installed manually as mentioned in [FAR docuementaion](https://github.com/medik8s/fence-agents-remediation#installation)

As opposed to other remediation systems, FAR requires credentials/access to a management interface (e.g., Intelligent Platform Management Interface ([IPMI](https://en.wikipedia.org/wiki/Intelligent_Platform_Management_Interface)), etc.) or an API to reboot a node, but it has many advantages.

### Advantages

* Robustness - FAR can remediate an unhealthy node using a management interface (e.g., IPMI) while still keeping control plane connectivity.
* Speed - FAR is fast as it adds the FAR NoExecute taint, and deletes workloads to accelerate workload rescheduling, in addition to rebooting the node using a fence agent.
* Diversity - FAR includes several FAs from a whole known set of upstream fencing agents for bare metal servers, virtual machines, cloud platforms, etc.
* Adjustability - FAR allows to set up of different parameters to access the management interface that remediates the node.
* Compatibility with NHC - FAR works with NHC to provide high availability for nodes in an automatic manner. NHC detects the node’s health and triggers FAR to remediate the node until it becomes healthy again.
* Standalone - FAR can be used as a standalone solution to remediate nodes with an administrator's help. Moreover, FAR is not limited to NHC and could work with another detection mechanism.
