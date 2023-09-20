---
layout: default
title: Remediation
nav_order: 4
has_children: true
---

## Putting Nodes into a Safe State (Remediation)

{: .no_toc }

### Table of contents

{: .no_toc .text-delta }

1. TOC
{:toc}

### The Problem

A common approach to for providing high availability for Kubernetes is to run
multiple copies of a service and starting replacements when any fail.  However
this approach cannot be applied for objects that require at-most-one semantics
like StatefulSets and RWO volumes.  Before we ask the scheduler to recover those
kinds of resources elsewhere, we must be certain that the "old" location not
only looks dead/down and not running them, but **is definitely** dead/down and not
running them.

### Remediation

At it's core, remediation (aka. fencing) turns a question _Can our peer cause
data corruption?_ into an answer _**No!**_ by isolating it both from incoming
requests and persistent storage.

Only after this is achieved do we become concerned with restoring cluster
capacity.

In cloud environments, where replacing a whole machine takes seconds, the most
common approach is to use something like 
[Machine API](https://github.com/kubernetes-sigs/cluster-api/blob/HEAD/docs/proposals/20181121-machine-api.md) 
to deprovision the failed node and replace it with a new one.

However not all k8s clusters come with the Machine API configured, and adding it
retrospectively is both complicated and not always possible and/or desirable.

Additionally, physical machines can't pop into existence via an API call and
take much longer to provision.

It is therefore clear that there is no one-size-fits-all solution for
remediation.  For this reason, the [ExternalRemediation API](https://github.com/kubernetes-sigs/cluster-api/blob/HEAD/docs/proposals/20191030-machine-health-checking.md)
was established to allow multiple remediation mechanisms to exist, even within a
single cluster, without creating conflicts.

### Implementations

Implementations conforming to the ExternalRemediation API include:

* [self-node-remediation](/remediation/self-node-remediation/self-node-remediation/) - a mechanism designed for shared-nothing environments without programmatic access to BMC-like hardware
* [(wip) metal3](https://github.com/metal3-io/cluster-api-provider-metal3/pull/157) - a mechanism designed for bare metal clusters with a functioning Metal3 API
* [machine-deletion-remediation](https://github.com/medik8s/machine-deletion-remediation) - a mechanism designed for any cluster with a functioning Machine API
* [fence-agents-remediation](https://github.com/medik8s/fence-agents-remediation) - a mechanism designed around an existing set of [upstream fencing agents](https://github.com/ClusterLabs/fence-agents) for environments with a traditional API end-point or a management interface (eg. IPMI) for power-cycling the cluster nodes
* (concept) meatware - a mechanism that includes explicit approval by a human
