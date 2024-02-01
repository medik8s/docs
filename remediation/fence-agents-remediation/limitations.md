---
layout: default
title: Limitations
parent: Fence Agents Remediation
grand_parent: Remediation
nav_order: 3
---

<!-- markdownlint-disable-next-line MD025 -->
# Limitations

1. Currently, FAR supports running a fence agent with only the *reboot* [action](https://github.com/ClusterLabs/fence-agents/blob/main/doc/FenceAgentAPI.md#agent-operations-and-return-values).
2. The running fence agent inside the FAR pod needs network connectivity to reach the unhealthy node interface, and fence it. In some platforms, the pod isn't granted with this kind of permission.
