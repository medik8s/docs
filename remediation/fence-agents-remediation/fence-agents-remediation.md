---
layout: default
title: Fence Agents Remediation
nav_order: 4
has_children: true
parent: Remediation
---

## Fence Agents Remediation

Generally Available
{: .label .label-green }

The [Fence Agents Remediation](https://github.com/medik8s/fence-agents-remediation#readme) (FAR) is a Kubernetes operator that uses external tools to *fence* unhealthy nodes.
The tools are a set of well-known [upstream fence agents](https://github.com/ClusterLabs/fence-agents), where each one of them can be used for different environments,
to fence a node using a traditional Application Programming Interface (API) call that reboots a node.
By doing FAR can minimizes downtime for stateful applications and restores compute capacity if transient failures occur.

FAR is not only fencing a node when it becomes unhealthy, it also tries to *remediate* the node from being unhealthy to healthy again.
It adds a taint to evict stateless pods, fence the node with a fence agent, and fully remediate it with resource deletion to remove any remaining workloads (mostly stateful workloads) after reboot.

FAR is recommended when a node becomes unhealthy, and we want to completely isolate the node from a cluster,
since we can’t “trust” the unhealthy node, to prevent it from accessing the shared resources like [RWO volumes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#access-modes).
The operator is available in the Kubernetes community, [OperatorHub.io](https://operatorhub.io/operator/fence-agents-remediation), and can be installed manually as mentioned in [FAR documentation](https://github.com/medik8s/fence-agents-remediation#installation)

Similar to the other [remediation operators from Medik8s](https://www.medik8s.io/remediation/remediation/#implementations),
FAR can semi-automate the node remediation once the node has been detected/selected to be remediated.
The selection can be done with the [Node HealthCheck Operator (NHC)](https://github.com/medik8s/node-healthcheck-operator#readme) which detects the node’s health,
another detection mechanism (or any other operator that supports an external remediation API), or even using an administrator’s help.
To fully automate a remediation process we can combine NHC with FAR, and automatically increase the availability of workloads.

As opposed to other remediation systems, FAR requires credentials for running the API call (e.g., Intelligent Platform Management Interface ([IPMI](https://en.wikipedia.org/wiki/Intelligent_Platform_Management_Interface)), etc.)
to reboot a node, but it has many advantages.

### Advantages

* Robustness - FAR can remediate an unhealthy node using a traditional API call (e.g., IPMI) while still keeping control plane connectivity.
* Speed - FAR is rapid since it can reboot a node and receive an acknowledgment from the API call while others might need to wait a safe time till they can expect the node to be rebooted.
Similarly to some other operators, FAR adds a NoExecute taint and deletes workloads to accelerate workload rescheduling, in addition to rebooting the node.
* Diversity - FAR includes several fence agents from a whole known set of upstream fencing agents for bare metal servers, virtual machines, cloud platforms, etc.
* Adjustability - FAR allows to set up different parameters for running the API call that remediates the node.
