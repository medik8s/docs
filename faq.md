---
layout: default
title: FAQ
nav_order: 9
---

# Frequently Asked Questions
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Does medik8s require OpenShift?

No.  Medik8s can run on any kubernetes cluster.

## Does medik8s require Machine API?

No.  Medik8s puts Nodes at the center of failure detection and recovery and can
run on any kubernetes cluster.

## Does medik8s require special hardware?

No.  While Medik8s can take advantage of hardware watchdogs and/or BMCs, it also
has options for shared-nothing recovery.

## What is the relationships to sig-cluster

The medik8s team has worked with the [sig-cluster community](https://github.com/kubernetes/community/tree/master/sig-cluster-lifecycle) for many years.
While we have many things in common, they are naturally focussed on furthering
the Machine/Cluster APIs.  Basing our solution on those APIs would limit the
types of clusters we can provide a solution for.

## What is the Relationships to Cluster/Machine API?

The original implementation put Machines at the center of failure detection and
exclusively used the [Machine API](https://github.com/kubernetes-sigs/cluster-api/blob/HEAD/docs/proposals/20181121-machine-api.md) for recovery.  Node Healthcheck Controller can
use the Machine API if it is available, but also supports other mechanisms.

### What is the connection to Machine Healthcheck Controller?

Apart from the medik8s team being actively involved with the [Machine Healthcheck
Controller](https://github.com/kubernetes-sigs/cluster-api/blob/master/controllers/machinehealthcheck_controller.go), the [Node Healthcheck Controller](https://github.com/medik8s/node-healthcheck-operator) also shares much of the same code.

The primary difference between the two implementations is putting Nodes at the
center of failure detection to avoid a dependancy on `Machine` objects, which
are not common to all kubernetes installations.

### What is the Relationships to External Remediation API?

The original MHC implementation assumed that using the Machine API to destroy
the bad node and replace it with a new one was the only necessary recovery
mechanism.

The medik8s team partnered with Ericsson to convince the sig-cluster community
that other mechanisms were needed (particularly on bare metal) and together we
created the External Remediation API that is used by both the Machine and Node
Healthcheck Controllers.

## Is a company behind this?

The medik8s team is employed at Red Hat, where we leverage 20 years of
traditional HA experience to create similar kubernetes native capabilities for
workloads such as Stateful sets and RWO Volumes.

## History

In 2018, the team behind medik8s prototyped what would eventually ship as the
Machine Healthcheck Controller for OpenShift 4.2.

Soon after, Red Hat brought the Machine Healthcheck Controller to sig-cluster
for consideration as a general purpose mechanism for detecting node failures and
recovering compute power and affected workloads.

In YEAR, for OpenShift 4.x, we improved support for bare metal by shipping an
annotation based mechansim for rebooting nodes instead of going through a time
expensive reprovisioning cycle.

In YEAR, we worked with Ericcson to design an official API for using mechanisms
to recover bad nodes.  Since then Ericcson has prototyped a
[metal3](http://metal3.io/) based implementation, and we have implemented
[Poison Pill](/PoisonPill) for shared-nothing environments.

In 2021, we drove the creation of medik8s to make general purpose HA available
to all kubernetes clusters, not just ones backed by an infrastructure API.

The combination of Node Healthcheck and Poison Pill is currently being validated
for production deployments and is expected to be live in a large cluster at a
Fortune ranked customer by the end of the year.
