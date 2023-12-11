---
layout: default
title: Fence Agents Remediation
nav_order: 4
has_children: true
parent: Remediation
---

<!-- markdownlint-disable-next-line MD025 -->
# Fence Agents Remediation

Generally Available
{: .label .label-green }

The [Fence Agents Remediation](https://github.com/medik8s/fence-agents-remediation#readme) (FAR) is a Kubernetes operator that uses external tools to *fence* unhealthy nodes.
The tools are a set of well-known [upstream fence agents](https://github.com/ClusterLabs/fence-agents), where each one of them can be used for different environments,
to fence a node using a traditional Application Programming Interface (API) call that reboots a node.
By doing so FAR can minimize downtime for stateful applications, restore compute capacity if transient failures occur, and increase the availability of workloads.

FAR is not only fencing a node when it becomes unhealthy, it also tries to *remediate* the node from being unhealthy to healthy again.
It adds a taint to evict stateless pods ([NoExecute](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/#taint-based-evictions)), fence the node with a fence agent,
and after reboot it completes the remediation with resource deletion to remove any remaining workloads (mostly stateful workloads).
Adding the taint and deleting the workloads accelerates the workload rescheduling.

FAR, similarly to the other [remediation operators from Medik8s](https://www.medik8s.io/remediation/remediation/#implementations), remediates an unhealthy node when its own
[custom resource (CR)](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/) is created for that node.
The node can be detected as unhealthy using the [Node HealthCheck Operator (NHC)](https://github.com/medik8s/node-healthcheck-operator#readme) which checks the node’s health
and automatically creates far CR when it is needed, another detection mechanism (or any other operator that supports an external remediation API), or even manually using an administrator’s help.
Moreover, FAR is available in the Kubernetes community, [OperatorHub.io](https://operatorhub.io/operator/fence-agents-remediation), and it can even be installed manually as mentioned in [FAR documentation](https://github.com/medik8s/fence-agents-remediation#installation).

In contrast to other remediation systems, FAR requires credentials for running the API call (e.g., Intelligent Platform Management Interface ([IPMI](https://en.wikipedia.org/wiki/Intelligent_Platform_Management_Interface)), etc.)
to reboot a node, but it has many advantages.

## Advantages

* Robustness - FAR has direct feedback from the traditional API call (e.g., IPMI) about the result of the fence action without using the Kubernetes API.
* Speed - FAR is rapid since it can reboot a node and receive an acknowledgment from the API call while others might need to wait a safe time till they can expect the node to be rebooted.
* Diversity - FAR includes several fence agents from a whole known set of upstream fencing agents for bare metal servers, virtual machines, cloud platforms, etc.
* Adjustability - FAR allows to set up different parameters for running the API call that remediates the node.
