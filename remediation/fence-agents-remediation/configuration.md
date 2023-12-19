---
layout: default
title: Configuration
parent: Fence Agents Remediation
grand_parent: Remediation
nav_order: 2
---

<!-- markdownlint-disable-next-line MD025 -->
# Fence Agents Remediation Configuration

Fence Agents Remediation (FAR) operator watches *FenceAgentsRemediation* (or *far*) Custom Resource ([CR](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/)).
Those CRs can be created either manually by cluster administrators, or by other operators (e.g., Node Health Check Operator [(NHC)](https://github.com/medik8s/node-healthcheck-operator#readme)) or simialr tools that trigger FAR by automatically creating far CRs using *FenceAgentsRemediationTemplate* (or *fartemplate*) CR.
FAR is recommended to be used with NHC.

## FAR with NHC

NHC needs to be configured to use FAR, thus a user must do the following steps:

* Install FAR and NHC
* Create fartemplate CR
* Create NHC CR to use fartemplate CR accordingly (see [NHC documentation](https://github.com/medik8s/node-healthcheck-operator/blob/main/docs/configuration.md#remediationtemplate)).

## FAR Standalone

* Install FAR
* Create far CR where the CR name should be the node to be remediated

The operator has many fence agents for different use cases, thus a user should choose the fence agent based on the cluster platform, and know its parameters for running FAR properly.
For more on how to configure and use FAR, please go to its [documentation](https://github.com/medik8s/fence-agents-remediation#usage).
