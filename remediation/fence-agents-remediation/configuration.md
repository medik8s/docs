---
layout: default
title: Configuration
parent: Fence Agents Remediation
grand_parent: Remediation
nav_order: 2
---

<!-- markdownlint-disable-next-line MD025 -->
# Fence Agents Remediation Configuration

Fence Agents Remediation (FAR) uses a Custom Resource (CR) created by [Node Health Check Operator](https://github.com/medik8s/node-healthcheck-operator#readme) (NHC) based on a FAR's remediation template (*FenceAgentsRemediationTemplate*).

NHC needs to be configured to use FAR, thus a user must do the following steps:

* Install FAR and NHC
* Create FAR Template CR
* Create NHC CR to use FAR Template CR accordingly (see [FAR documentation](https://github.com/medik8s/fence-agents-remediation#far-with-nhc)).
