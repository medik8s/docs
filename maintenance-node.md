---
layout: default
title: Maintenance
nav_order: 6
---

# Place Nodes in Maintenance Mode
{: .no_toc }
## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## The Problem

Nodes in a Kubernetes cluster (especially bare metal nodes) face many problems, and they can fail due to a kernel error or a NIC card hardware failure.
The workloads on the failed node need to be restarted on another node in the cluster while the problem node is repaired or replaced.

## The Solution
[Node Maintenance Operator (NMO)](https://github.com/medik8s/node-maintenance-operator) is an open source Kubernetes operator which keeps nodes cordoned and drained while a matching NodeMaintenance (nm) custom resource (CR) exists.

Generally Available
{: .label .label-green }
<img src="../images/operator-icon/nmo_blue_icon.png" alt="nmo-icon" width="150" style="margin-left:auto; margin-right:auto; display:block"/>

The operator perform a declarative way for doing [`kubectl cordon NODE`](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#cordon) (set node as unschedulable), 
[`kubectl drain NODE`](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#drain) (evict pods from node), and [`kubectl taint NODE NAME KEY_1=VAL_1:TAINT_EFFECT_1`](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#taint) (add taint for node).
The operator watches for new or deleted CRs which indicate that a node in the cluster should be placed into maintenance when nm CR has been created, or should end maintenance when nm CR has been deleted.
When the node is in maintenance mode, then it is cordoned - set as unschedulable, and all the (possible) pods are drained (evicted) from that node.
When the node leaves maintenance mode, then it is uncordoned - set as schedulable.
Detailed progress and node status details are provided during maintenance.

## Usage
The operator can be installed from [OperatorHub](https://operatorhub.io) or [built and run from source](https://github.com/medik8s/node-maintenance-operator#build-and-run-the-operator).
See [NMO's Readme](https://github.com/medik8s/node-maintenance-operator#setting-node-maintenance) for how to set/unset the node into maintenance mode, and also for better understanding of the [nm CR status](https://github.com/medik8s/node-maintenance-operator#nodemaintenance-status).
