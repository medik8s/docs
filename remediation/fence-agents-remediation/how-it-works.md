---
layout: default
title: How It Works
parent: Fence Agents Remediation
grand_parent: Remediation
nav_order: 1
---

<!-- markdownlint-disable-next-line MD025 -->
# How does Fence Agents Remediation work?

The Fence Agents Remediation [(FAR)](https://github.com/medik8s/fence-agents-remediation#readme) uses external tools to *fence* unhealthy nodes.
These tools are a set of well-known [upstream fence agents](https://github.com/ClusterLabs/fence-agents), where each fence agent can be used for different environments to fence a node, and using a traditional Application Programming Interface (API) call that reboots a node. By doing so, FAR can minimize downtime for stateful applications, restores compute capacity if transient failures occur, and increases the availability of workloads.

FAR uses a fence agent to fence a Kubernetes node. Generally, fencing is the process of taking unresponsive/unhealthy servers into a safe state and isolating the server. Fence agent is an application that uses an API call to perform fencing, mostly power-based fencing which enables power-cycling, resetting, or turning off the server.

FAR not only fences a node when it becomes unhealthy, it also tries to *remediate* the node from being unhealthy to healthy. It adds a taint to evict stateless pods ([NoExecute](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/#taint-based-evictions)), fences the node with a fence agent, and after a reboot, it completes the remediation by evicting the remaining workloads (mostly stateful workloads). Adding the taint and deleting the workloads accelerates the workload rescheduling.

FAR, similarly to the other [remediation operators from Medik8s](https://www.medik8s.io/remediation/remediation/#implementations), remediates an unhealthy node when its own [custom resource (CR)](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/) is created for that node. The node can be detected as unhealthy using the [Node HealthCheck Operator (NHC)](https://github.com/medik8s/node-healthcheck-operator#readme) which will create far CRs automatically when it is needed, or another detection mechanism (or any other operator that supports an external remediation API).
Furthermore, it can also be done manually using an administrator’s help.

For more on how FAR operator works, please go to its [documentation](https://github.com/medik8s/fence-agents-remediation#how-does-far-work).
