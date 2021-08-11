---
layout: default
title: Workload Recovery
nav_order: 8
---

# Recovering Affected Workloads

In kubernetes world there is no concept of rescheduling. When pods are bounded to a
node they run till termination. In a case of hardware failure, or some other
resource problem that hang the OS, there is no built-in solution to migrate or
restart existing pods.

If the node misbehaves, and processes can not run anymore the control
plane will start counting down. It will either be the kubelet process which doesn't
report status to the control plane [(see node_status_update_frequency)][1] or
the containers themselves will fail/crash and be marked as `phase: failed`.
Nodes status conditions, set by the node-controller in the control plane, will
reflect now what's happening and for how long.
For example, in the case where the node fails to update its status to the
masters the node condition will be set to `type:Ready status:Unknown`.

In order to gain the workload back, reschedule it and start it all over, the
control plane needs to know that the running node is gone and the only way to achieve
that is by deleting the node object, which will trigger [scheduling the pods for
deletion][2]

The job of [poison-pill]() is to reboot a failing host, delete its node object,
,and recreate it to restore the node to a working state.

# Pod recovery flow

After the node is deleted, a pod is scheduled for deletion by the control
plane. Then, depending on deployment kind, a new pod with the same spec
will be created.

# Volume recovery flow

Regular volumes attached to pod are ephemeral and don't contain persisted data.
They are mostly used to mount secretes, config maps, share unix sockets between
components and maybe temporary storage of data. Recovering them is not considered
an issue.
Persistent volumes however are the main concern of workload that is lost.
For persistent volumes from a CSI driver, the spec defines that a deletion pod
will trigger the deletion of `VolumeAttachment`, which will trigger unmounting
the volume from the underlying storage system - a unique operation per driver provider.
After a successful unpublishing the pod and the volume can start again, on a different
node.

## Virtualized worker note
Nodes which are VMs should be configured with a watchdog device ([see libvirt's watchdog support][3])
In case it's not configured then poison-pill fallbacks to rebooting the machine
using 'systemctl reboot'. The benefits of a virtualized watchdog is that its running
on the hypervisor and is not vulnerable to resource starvation problem in the VM level
resulting a quicker reboot action.

# Statefulset recovery flow

TBD

[1]: https://kubernetes.io/docs/reference/command-line-tools-reference/kubelet/
[2]: https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/#pod-garbage-collection
[3]: https://libvirt.org/formatdomain.html#watchdog-device
