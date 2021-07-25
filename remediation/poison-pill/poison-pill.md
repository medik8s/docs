---
layout: default
title: Poison Pill
nav_order: 1
has_children: true
parent: Remediation
---

# Node Remediation with Poison Pill

Poison Pill is an open-source remediation system that runs as a Daemonset - a pod per node, which reboots unhealthy nodes.
Node Healthceck Operator (or any other operator that supports the external remediation API) will create 
a PoisonPillRemediation CR for an unhealthy node. The Poison Pill agent will reboot once this CR exists.

As opposed to other remediation systems, Poison Pill does not require any management interface (e.g. IPMI etc.)

## How Poison Pill is Different from Other Solutions?
The existing remediation solutions have some limitations, assumptions or pre-requisites that do not apply to Poison Pill:

* The unhealthy node should be able to contact the API-Server
* The cluster should have been provisioned with some way to interact with the infrastrcture provider (such as Cluster-API Machines)
* The control plane should have connectivity to the unhealthy node's management interface

Poison Pill doesn't have any of this limitations and has no pre-requisites


## Source Code
Poison Pill is open source: [Github Repo](https://github.com/medik8s/poison-pill)

