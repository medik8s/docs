---
layout: default
title: Configuration
parent: Machine Deletion
grand_parent: Remediation
nav_order: 2
---

# Machine Deletion Remediation Configuration
Machine Deletion Remediation (MDR) uses a Custom Resource (CR) created by [Node Health Check](https://github.com/medik8s/node-healthcheck-operator#readme) (NHC) based on a specific template.
Since NHC comes with Self Node Remediation as the default remediation mechanism, it needs to be configured to use MDR; hence the following is required:
1. Create the MDR Template CR using the provided [manifest](https://github.com/medik8s/machine-deletion#example-crs)
2. Modify NHC CR to [use MDR as it's remediator](https://github.com/medik8s/machine-deletion#example-crs)
