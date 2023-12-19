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

The [Fence Agents Remediation](https://github.com/medik8s/fence-agents-remediation#readme) (FAR) is a Kubernetes operator that uses well-known agents to fence and remediate unhealthy nodes.
The remediation includes rebooting the unhealthy node using a fence agent and then evicting workloads from the unhealthy node.

FAR is available in the Kubernetes community, [OperatorHub.io](https://operatorhub.io/operator/fence-agents-remediation), or it can be installed manually as mentioned in [FAR documentation](https://github.com/medik8s/fence-agents-remediation#installation).

## Advantages

* Robustness - FAR has direct feedback from the traditional Application Programming Interface (API) call (e.g., [IPMI](https://en.wikipedia.org/wiki/Intelligent_Platform_Management_Interface)) about the result of the fence action without using the Kubernetes API.
* Speed - FAR is rapid since it can reboot a node and receive an acknowledgment from the API call while other remediators might need to wait a safe time till they can expect the node to be rebooted.
* Diversity - FAR includes several fence agents from a large known set of upstream fencing agents for bare metal servers, virtual machines, cloud platforms, etc.
* Adjustability - FAR allows to set up different parameters for running the API call that remediates the node.
