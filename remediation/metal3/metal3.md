---
layout: default
title: Metal3
nav_order: 2
has_children: false
parent: Remediation
---

# Metal3 Power Based Remediation 
work-in-progress
{: .label }

[metal3](http://metal3.io/) is a CNCF project that provides a bare metal hosts provisioning, which integrates with the Machine API.
Unlike cloud providers, reprpovisioning a bare metal host could be a long operation, during which the stateful applications are down.
To recover workloads quickly, the Metal3 power based remediator will fence the node by shutting it off, deleting the node object, and power the host back on.

## Metal Power based remediators vs Poison Pill

There are some key differences between the metal3 based remediator and Poison Pill.
The metal3 project requires a valid BMC credentials, and remediation requires a working access of the BMC API, while the node is unhealthy.
The BMC API might be down for several reasons, e.g. power issues, which prevents remediation and workload recovery.

The Poison Pill Operator doesn't require any BMC credntials/access but relies on some heuristics. The metal3 power based remediation is more robust and determinstic.

