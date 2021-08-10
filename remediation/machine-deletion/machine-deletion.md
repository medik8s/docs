---
layout: default
title: Machine Deletion
nav_order: 3
has_children: true
parent: Remediation
---

# Machine-API Driven Remediation
Generally Available
{: .label .label-green }

This operator conforms to the External Remediation of [NodeHealthCheck](https://github.com/medik8s/node-healthcheck-operator#readme) and is designed to work with [Node Health Check]((https://github.com/medik8s/node-healthcheck-operator#readme)) to reprovision unhealthy nodes using the [Machine API](https://github.com/openshift/machine-api-operator#readme). It functions by following the annotation on the Node to the associated Machine object, confirms that it has an owning controller (e.g. MachineSetController), and deletes it.  Once the Machine CR has been deleted, the owning controller creates a replacement. 
