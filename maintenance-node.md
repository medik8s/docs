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

<img src="../images/operator-icon/nmo_blue_icon.png" alt="nmo-icon" width="150" style="margin-left:auto; margin-right:auto; display:block"/>

## The Problem

Nodes in a Kubernetes cluster (especially bare meteal nodes) face many problems, and they can fail due to a kernel error or a NIC card hardware failure. The workloads on the failed node need to be restarted on another node in the cluster while the problem node is repaired or replaced. Node maintenance mode allows cluster administrators to gracefully turn-off nodes, move workloads to other parts of the cluster, and ensure that workloads do not get interrupted. Detailed progress and node status details are provided during maintenance.

## Maintenance Mode
Node Maintenance Operator (NMO) is an open soucrce Kubernetes operator which keep nodes cordoned and drained while a matching NodeMaintenance (nm) custom resource (CR) exists.

The operator watches for new or deleted CRs which indicate that a node in the cluster should move into maintenance when nm CR has been created or outisde of maintenance when nm CR has been deleted.
When the node is in maintanince mode, then it is cordoned - set as unschedulable, and all the (possible) pods are evicted from that node.
When the node leaves maintenance mode, then it is uncordoned - set as schedulable, and the NMO pod is removed.

Previously NMO was developed and bundled in KubeVirt project (or [OpenShift Virtualization](https://docs.openshift.com/container-platform/latest/virt/about-virt.html)).


## Usage
The operator can be installed using OperatorHub or [built and run from source](https://github.com/medik8s/node-maintenance-operator#build-and-run-the-operator).
See in [here](https://github.com/medik8s/node-maintenance-operator#setting-node-maintenance) how to set/unset the node into maintenance mode, and also to understand [nm CR status](https://github.com/medik8s/node-maintenance-operator#nodemaintenance-status).

In addition, OpenShift users can use NMO directly from the Red Hat catalog (please see Node Maintenance Operator documnetaion in [OpenShfit Container Platform (OCP)](https://docs.openshift.com/container-platform/latest/nodes/nodes/eco-node-maintenance-operator.html)).
