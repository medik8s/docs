---
layout: default
title: Failure Detection
nav_order: 3
---

# Detecting Node Failures 
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

A Node entering an unready state after 5 minutes is an obvious sign that a
failure occurred, but depending on your physical environment, workloads, and
tolerance for risk, there may be other criteria or thresholds that are
appropriate.

## Node Healthcheck Controller

The [Node Healthcheck Controller](https://github.com/medik8s/node-healthcheck-operator) checks each Node's set of [NodeConditions](https://kubernetes.io/docs/concepts/architecture/nodes/#condition)
against the criteria and thresholds defined for it in [NodeHealthCheck](https://github.com/medik8s/node-healthcheck-operator#nodehealthcheck-custom-resource) CRs.
If the Node is deemed to be in a failed state, and remediation is appropriate,
the controller will instantiate a RemediationRequest template (defined as part
of the CR) that specifies the mechansim/controller to be used for recovery.

Should the Node recover on its own, the NH controller removes the instantiated
RemediationRequest.  In all other respects, the RemediationRequest is owned by
the [target remediation mechanism](../remediation) and will persist until that controller is
satisfied remediation is complete.  For some mechanisms that may mean the Node
has entered a safe state (eg. the underlying "hardware" has been deprovisioned),
for others it may be the Node coming back online (eg. after a reboot).

Remediation is not always the correct response to a failure.  Especially in
larger clusters, we want to protect against failures that appear to take out
large portions of compute capacity but are really the result of failures on or
near the control plane.

For this reason, the healthcheck CR includes the ability to define a percentage
or total number of nodes that can be considered candidates for concurrent
remediation.

## Background
See the [FAQ](/FAQ)
