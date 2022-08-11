---
layout: default
title: Self Node Remediation
nav_order: 1
has_children: true
parent: Remediation
---

# Node Remediation with Self Node Remediation
Generally Available
{: .label .label-green }

<img src="../../../images/operator-icon/snr_icon_blue.png" alt="snr-icon" width="150" style="margin-left:auto; margin-right:auto; display:block"/>

Self Node Remediation is an open-source remediation system that runs as a Daemonset - a pod per node, which reboots unhealthy nodes.
`Node Healthcheck Operator` (or any other operator that supports the external remediation API) will create 
a `SelfNodeRemediation` custom resource for an unhealthy node. The Self Node Remediation agent will reboot once this custom resource exists.

As opposed to other remediation systems, Self Node Remediation does not require any management interface (e.g. IPMI etc.) or an API to node provisioning.
