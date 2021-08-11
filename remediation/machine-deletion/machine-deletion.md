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

This operator conforms to the External Remediation of [NodeHealthCheck](https://github.com/medik8s/node-healthcheck-operator#readme) and is designed to work with it in order to reprovision unhealthy nodes using the [Machine API](https://github.com/openshift/machine-api-operator#readme). 
It looks for the associated Machine of an unhealthy Node, and deletes it.  
Once the Machine CR has been deleted, the owning controller creates a replacement. 
