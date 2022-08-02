---
layout: default
title: FAQ
parent: Self Node Remediation
grand_parent: Remediation
nav_order: 3
---

# Frequently Asked Questions
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## How Self Node Remediation Reboots a Node?
We encourage users to utilize a watchdog device, which will be able to reboot the node even in the case of resource starvation or bugs that may exist.
In nodes without a hardware wathcdog device, softdog is preferred.
In the absence of a valid watchdog device, self node remediation will use forced software reboot.

## Why does Self Node Remediation contact other nodes?
In the case of issues which prevent getting responses from the api-server, there’s no way for the self-node-remediation agent to know if it’s healthy or not.
If we would have ignored this situation, the other nodes could assume the unhealthy node has been rebooted and delete the node while it’s still running.
To overcome this, the node queries the other nodes and uses them as a proxy to the api-server, so they can tell if it’s healthy or not.
If the other nodes can’t access the api-server as-well, we assume this is an api-server failure and do nothing.

## What actions are taken by the healthy nodes once there’s an unhealthy node?
The nodes will mark the unhealthy node as unschedulable, backup the node resource in the SNR (SelfNodeRemediation) so we can restore the node later, and delete the node object which signals to the cluster that the workloads can be safely rescheduled elsewhere.

## Why does Self Node Remediation restore the node? Why are we not doing it in power-based remediation?
In power based remediation we delete the node once the host is powered off. Once the host is powered on again, it would register itself in the cluster.
In Self Node Remediation, we can’t keep the host powered off (we don’t have [BMC](https://en.wikipedia.org/wiki/Intelligent_Platform_Management_Interface#Baseboard_management_controller) credentials/access), so the node is deleted when the unhealthy node is powered-on. Kubelet will only register itself when it boots. So once the node is deleted, it will never come back unless we restore it.
The unhealthy life-cycle flow can be described as follows:
1. Node x becomes unhealthy.
2. Node x reboots.
3. Node x boots, the node object already exists in the cluster (nothing deleted it at this point).
4. Other node deletes the unhealthy node.

## What are the Self Node Remediation CRDs and what’s their purpose?
Self Node Remediation has 3 CRDs:
* SelfNodeRemediationConfig - automatically created by the operator. Contains configuration for the self node remediation daemonset, and can be modified by the user.
* SelfNodeRemediation - the health detection system (e.g. MHC/NHC) should create instance of this CR to signal that a node/machine is unhealthy.
* SelfNodeRemediationTemplate - automatically created by the operator and should be referenced in the MHC/NHC CR. This is currently empty but we might be used to pass some remediation configuration.

## Does Self Node Remediation work on its own as a standalone operator?
Self Node Remediation is a remediation/fencing system. It doesn’t provide any health detection system.
Self node remediation is a consumer of the external remediation API, and responds to health issues reported by that API.
Note that in the case of a node that can’t contact any of the nodes, the self node remediation will trigger remediation without relying on any health detection system.

## How Self Node Remediation is Different from Other Solutions?
The existing remediation solutions have some limitations, assumptions or prerequisites that do not apply to Self Node Remediation:

* The unhealthy node should be able to contact the API-Server
* The cluster should have been provisioned with some way to interact with the infrastructure provider (such as Cluster-API Machines)
* The control plane should have connectivity to the unhealthy node's management interface

Self Node Remediation doesn't have any of these limitations and has no prerequisites

## Where Can I Find the Source Code?
Self Node Remediation is open source: [Github Repo](https://github.com/medik8s/self-node-remediation)

