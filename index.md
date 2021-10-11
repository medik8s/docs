---
layout: default
title: Home
nav_order: 1
---

<img src="images/medik8s-logo.png" alt="medik8s-logo" width="300" style="margin-left:auto; margin-right:auto; display:block"/>

# Medik8s - Kubernetes Node Remediation
{: .fs-8 }

Medik8s is a project consists of several kubernetes operators that provide automatic node remediation and high availability for singleton workloads
{: .fs-6 .fw-300 }


[Get started now](/GettingStarted){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 }
[Demo](/Demo){: .btn .btn-green }

Hardware is imperfect, and software contains bugs. When node level failures such
as kernel hangs or dead NICs occur, the work required from the cluster does not
decrease - workloads from affected nodes need to be restarted somewhere.

However some workloads, such as RWO volumes and StatefulSets, may require
at-most-one semantics.  Failures affecting these kind of workloads risk data
loss and/or corruption if nodes (and the workloads running on them) are assumed
to be dead whenever we stop hearing from them.  For this reason it is important
to know that the node has reached a safe state before initiating recovery of the
workload.

Unfortunately it is not always practical to require admin intervention in order
to confirm the node's true status. In order to automate the recovery of exclusive
workloads, Medik8s presents a collection of projects that can be installed on any
kubernetes-based cluster to automate:
* the [detection of failures](failure_detection),
* putting [nodes into a safe state](/remediation/remediation),
* allowing the scheduler to [recover affected workloads](recover_affected_workloads)
* attempting to [restore cluster capacity]()

## Community
Join [our google group](https://groups.google.com/g/medik8s) to get more info, participate in dicussions and get notified
for new releases

<script type="text/javascript">
function openRemediationMenu(){
  document.getElementsByClassName("nav-list-item")[3].classList.add("active")
 }
document.body.addEventListener("load", openRemediationMenu(), false);
</script>
