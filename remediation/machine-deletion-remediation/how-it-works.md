---
layout: default
title: How It Works
parent: Machine Deletion Remediation
grand_parent: Remediation
nav_order: 1
---

# How Machine Deletion Remediation works?
Machine Deletion Remediation (MDR) uses the [Machine API](https://github.com/openshift/machine-api-operator#readme) to reprovision unhealthy nodes.
It was tested with [NodeHealthCheck](https://github.com/medik8s/node-healthcheck-operator#readme) (NHC), which creates a Custom Resource for MDR with information about the unhealthy Node.

MDR follows the annotation on the Node to the associated Machine object, confirms that it has an *owning controller* (e.g. MachineSetController), that will recreate the Machine once deleted, and then proceeds with the deletion of the Machine.
