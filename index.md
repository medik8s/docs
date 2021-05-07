![medik8s logo](images/medik8s-logo.png "Medik8s Logo")

## Medik8s - High Availability for Singleton Workloads

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
* putting [nodes into a safe state](remediation),
* allowing the scheduler to [recover affected workloads]()
* attempting to [restore cluster capacity]()
