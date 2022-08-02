---
layout: default
title: Configuration
parent: Self Node Remediation
grand_parent: Remediation
nav_order: 2
---

# Self Node Remediation Configuration
Self Node Remediation utilizes a custom resource (CR) to define a custom configuration.
The `SelfNodeRemediationConfig` CR is automatically created upon installation.
Currently there are two configuration fields:
1. Watchdog device - the file path of the watchdog in the nodes. If this path doesn't exist, Self Node Remediation will use a software reboot.
2. Safe timeout - Self Node Remediation needs to assume the timeout that a unhealthy node has been rebooted. Self Node Remediation automatically calculates the lower bound for this value, but it can and should be changed to an upper value, in case of non-homogenous hardware where different nodes have different watchdog timeout.

The `SelfNodeRemediationConfig` CR will be created at the same namespace of the operator, with the name `self-node-remediation-config`.
A user may edit this CR but not create a new one.

Any change to the `SelfNodeRemediationConfig` CR will result in re-creation of the Self Node Remediation daemonset.
