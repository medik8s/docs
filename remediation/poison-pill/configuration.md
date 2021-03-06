---
layout: default
title: Configuration
parent: Poison Pill
grand_parent: Remediation
nav_order: 2
---

# Poison Pill Configuration
Poison Pill utilizes a custom resource (CR) to define a custom confiugration.
The `PoisonPillConfig` CR is automatically created upon installation.
Currently there are two configuration fields:
1. Watchdog device - the file path of the watchdog in the nodes. If this path doesn't exist, Poison Pill will use a software reboot.
2. Safe timeout - Poison Pill needs to assume the timeout that a unhealthy node has been rebooted. Poison Pill automatically calculates the lower bound for this value, but it can and should be changed to an upper value, in case of non-homogenous hardware where different nodes have different watchdog timeout.

The `PoisonPillConfig` CR will be created at the same namespace of the operator, with the name `poison-pill-config`.
A user may edit this CR but not create a new one.

Any change to the `PoisonPillConfig` CR will result in re-creation of the Poison Pill daemonset.
