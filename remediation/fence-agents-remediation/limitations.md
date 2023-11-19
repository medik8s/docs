---
layout: default
title: Limitations
parent: Fence Agents Remediation
grand_parent: Remediation
nav_order: 3
---

<!-- markdownlint-disable-next-line MD025 -->
# Limitations

1. FAR is limited to running fence agents with only one [action](https://github.com/ClusterLabs/fence-agents/blob/main/doc/FenceAgentAPI.md#agent-operations-and-return-values), reboot.
2. FAR remediation time can be long when the FAR pod resides in the unhealthy node since the FAR pod needs to be rescheduled on a different node.
