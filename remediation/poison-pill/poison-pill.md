---
layout: default
title: Poison Pill
nav_order: 1
has_children: true
parent: Remediation
---

# Node Remediation with Poison Pill
Generally Available
{: .label .label-green }

Poison Pill is an open-source remediation system that runs as a Daemonset - a pod per node, which reboots unhealthy nodes.
`Node Healthceck Operator` (or any other operator that supports the external remediation API) will create 
a `PoisonPillRemediation` custom resource for an unhealthy node. The Poison Pill agent will reboot once this custom resource exists.

As opposed to other remediation systems, Poison Pill does not require any management interface (e.g. IPMI etc.) or an API to node provisioning.
