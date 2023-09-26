---
layout: default
title: How It Works
parent: Fence Agents Remediation
grand_parent: Remediation
nav_order: 1
---

## How Fence Agents Remediation works?

Fence Agents Remediation (*FAR*) operator uses a management interface or a traditional API to remediate unhealthy kubernetes nodes.
It was tested with [Node HealthCheck Operator](https://github.com/medik8s/node-healthcheck-operator) (NHC), that creates a Custom Resource (CR) for FAR with information about the unhealthy Node.

FAR remediates a node by rebooting an unhealthy node, and moving any remaining workloads from the node to other nodes, so they can be processed in other nodes and be isolated from the unhealthy node. The reboot is done by executing a fence agent for the unhealthy node, while evicting the workloads from this node is achieved by tainting the node and deleting the workloads.

FAR uses a fence agent to fence a Kubernetes node. Generally, fencing is the process of taking unresponsive/unhealthy computers into a safe state and isolating the computer. Fence agent is a software code that uses a management interface to perform fencing, mostly power-based fencing which enables power-cycling, resetting, or turning off the computer. FAR includes some of the fence agents from the [upstream repository](https://github.com/ClusterLabs/fence-agents) by the *ClusterLabs* group.

For more on how FAR operator works, please go to its [documentation](https://github.com/medik8s/fence-agents-remediation#how-does-far-work).
