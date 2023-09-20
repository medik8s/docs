---
layout: default
title: Configuration
parent: Fence Agents Remediation
grand_parent: Remediation
nav_order: 2
---

## Fence Agents Remediation Configuration

Fence Agents Remediation (FAR) uses a Custom Resource (CR) created by [Node Health Check Operator](https://github.com/medik8s/node-healthcheck-operator#readme) (NHC) based on a specific remediation template (*FenceAgentsRemediationTemplate*).

Since NHC comes with [Self Node Remediation](https://www.medik8s.io/remediation/self-node-remediation/self-node-remediation/) as the default remediation mechanism, it needs to be configured to use FAR. Thus a user must do the following steps:

* Install FAR and NHC
* Create FAR Template CR
* Create NHC CR to use FAR Template CR accordingly (see [FAR documentation](https://github.com/medik8s/fence-agents-remediation#far-with-nhc)).
