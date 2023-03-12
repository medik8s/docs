---
layout: default
title: About Us
nav_order: 10
---

# About Us
{: .no_toc }
## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

<img src="../images/medik8s-logo.png" alt="nmo-icon" width="200" style="margin-left:auto; margin-right:auto; display:block"/>

## Who are we?

We are small team of Red Hatters with a strong passion to High Availability (HA) solutions in the Kubernetes world.

## What we do?

We develop Kubernetes Open Source Operators using [Operator Lifecycle Manager (OLM)](https://olm.operatorframework.io/) that provide maintenance support, automatic node remediation and high availability for singleton workloads:

- [Node Healthcheck Operator (NHC)](failure_detection) - Detecting Node Failures, triggering remediation, which is performed by other operators like Self Node Remediation or Machine Deletion Remediation.
- [Self Node Remediation (SNR)](/remediation/self-node-remediation/self-node-remediation) - Remediates nodes by rebooting, without needing a management interface like e.g. IPMI, or a node / machine provisioning API. Works standalone, and / or with NHC.
- [Node Maintenance Operator (NMO)](maintenance-node) - Declarative node cordoning and draining prior to harmful decisions.

## What we plan to do?

We have few work in progress operators:

- [Machine Deletion Remediation](/remediation/machine-deletion/machine-deletion-remediation) - Remediates nodes by deleting the associated OpenShift machine. Triggered by NHC.
- [HA-SNO](https://github.com/medik8s/ha-sno) - High Availability based on two Single Node OpenShift.

## History

In 2018, the team behind Medik8s prototyped what would eventually ship as the
Machine Healthcheck Controller for OpenShift 4.2.

Soon after, Red Hat brought the Machine Healthcheck Controller to sig-cluster
for consideration as a general purpose mechanism for detecting node failures and
recovering compute power and affected workloads.

In 2019, we improved support for bare metal by shipping an
annotation based mechanism for rebooting nodes instead of going through a time
expensive reprovisioning cycle.

In 2020, we worked with Ericsson to design an official API for using alternative
mechanisms to recover bad nodes.  Since then Ericsson has prototyped a
[metal3](http://metal3.io/) based implementation, and we have implemented
[Poison Pill (PP)](https://github.com/medik8s/poison-pill) for shared-nothing environments.

In 2021, we created Medik8s to make general purpose HA available
to all kubernetes clusters, not just ones backed by an infrastructure API.
Afterwards, we have implemented [Node Healthcheck Operator](https://github.com/medik8s/node-healthcheck-operator) 
which detects the node's health and deploy with PP to remediate the node.

In 2022, we have moved Node Maintenance Operator from [KubeVirt project](https://github.com/kubevirt/node-maintenance-operator) 
to [Medik8s project](https://github.com/medik8s/node-maintenance-operator) 
which is a declarative way for node cordoning and draining.
Moreover, we have renamed [Poison Pill](https://github.com/medik8s/poison-pill) project to 
[Self Node Remediation](https://github.com/medik8s/self-node-remediation) project.

## Community
Join [our google group](https://groups.google.com/g/medik8s) to get more info, participate in discussions and get notified
for new releases
