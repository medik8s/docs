---
layout: default
title: Known Issues
parent: Fence Agents Remediation
grand_parent: Remediation
nav_order: 4
---

<!-- markdownlint-disable-next-line MD025 -->
# Known Issues

1. FAR can't be updated from v0.1.0 to any newer versions.
2. Currently, FAR remediation time can be long when the FAR pod resides in the unhealthy node since the FAR pod needs to be rescheduled on a different node.
