---
layout: default
title: How It Works
parent: Fence Agents Remediation
grand_parent: Remediation
nav_order: 1
---

<!-- markdownlint-disable-next-line MD025 -->
# How does Fence Agents Remediation work?

The Fence Agents Remediation (FAR) operator uses a traditional API to remediate unhealthy Kubernetes nodes.
It is designed to be used with [Node HealthCheck Operator](https://github.com/medik8s/node-healthcheck-operator) (NHC),
which creates a Custom Resource (CR) for FAR with information about the unhealthy Node.
The remediation includes rebooting the unhealthy node using a fence agent and evicting workloads from the unhealthy node by resource deletion.

FAR uses a fence agent to fence a Kubernetes node. Generally, fencing is the process of taking unresponsive/unhealthy servers into a safe state and isolating the server.
Fence agent is a software code that uses an Application Programming Interface (API) call to perform fencing, mostly power-based fencing which enables power-cycling, resetting, or turning off the server.
FAR includes some of the fence agents from the [upstream repository](https://github.com/ClusterLabs/fence-agents) by the *ClusterLabs* group.

For more on how FAR operator works, please go to its [documentation](https://github.com/medik8s/fence-agents-remediation#how-does-far-work).
