---
layout: default
title: FAQ
parent: Poison Pill
grand_parent: Remediation
nav_order: 2
---

# Frequently Asked Questions
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## How Poison Pill Reboots a Node?
We encourage users to utilize a watchdog device, which will be able to reboot the node even in the case of resource starvation or bugs that may exist.
In nodes without a hardware wathcdog device, softdog is prefered.
In the absence of a valid watchdog device, poison pill will use forced software reboot.

## Why does Poison Pill contact other nodes?
In the case of issues which prevent getting responses from the api-server, there’s no way for the poison-pill agent to know if it’s healthy or not.
If we would have ignored this situation, the other nodes could assume the unhealthy node has been rebooted and delete the node while it’s still running.
To overcome this, the node queries the other nodes and uses them as a proxy to the api-server, so they can tell if it’s healthy or not.
If the other nodes can’t access the api-server as-well, we assume this is an api-server failure and do nothing.

## What actions are taken by the healthy nodes once there’s an unhealthy node?
The nodes will mark the unhealthy node as unschedulable, backup the node resource in the PPR (PoisonPillRemediation) so we can restore the node later, and delete the node object which signals to the cluster that the workloads can be safely rescheduled elsewhere.

## Why does Poison Pill restore the node? Why are we not doing it in power-based remediation?
In power based remediation we delete the node once the host is powered off. Once the host is powered on again, it would register itself in the cluster.
In Poison Pill, we can’t keep the host powered off (we don’t have [BMC](https://en.wikipedia.org/wiki/Intelligent_Platform_Management_Interface#Baseboard_management_controller) credentials/access), so the node is deleted when the unhealthy node is powered-on. Kubelet will only register itself when it boots. So once the node is deleted, it will never come back unless we restore it.
The unhealthy life-cycle flow can be described as follows:
1. Node x becomes unhealthy.
2. Node x reboots.
3. Node x boots, the node object already exists in the cluster (nothing deleted it at this point).
4. Other node deletes the unhealthy node.

## What are the Poison Pill CRDs and what’s their purpose?
Poison Pill has 3 CRDs:
* PoisonPillConfig - automatically created by the operator. Contains configuration for the poison pill daemonset, and can be modified by the user.
* PoisonPillRemediation - the health detection system (e.g. MHC/NHC) should create instance of this CR to signal that a node/machine is unhealthy.
* PoisonPillRemediationTemplate - automatically created by the operator and should be referenced in the MHC/NHC CR. This is currently empty but we might be used to pass some remediation configuration.

## Does Poison Pill work on its own as a standalone operator?
Poison Pill is a remediation/fencing system. It doesn’t provide any health detection system.
Poison pill is a consumer of the external remediation API, and responds to health issues reported by that API.
Note that in the case of a node that can’t contact any of the nodes, the poison pill will trigger remediation without relying on any health detection system.

## How Poison Pill is Different from Other Solutions?
The existing remediation solutions have some limitations, assumptions or prerequisites that do not apply to Poison Pill:

* The unhealthy node should be able to contact the API-Server
* The cluster should have been provisioned with some way to interact with the infrastrcture provider (such as Cluster-API Machines)
* The control plane should have connectivity to the unhealthy node's management interface

Poison Pill doesn't have any of this limitations and has no prerequisites

## Where Can I Find the Source Code?
Poison Pill is open source: [Github Repo](https://github.com/medik8s/poison-pill)

