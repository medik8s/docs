---
layout: default
title: Workload Recovery
nav_order: 8
---

# Recovering Affected Workloads

In kubernetes world there is no concept of rescheduling. When pods are bounded to a
node they run till termination. In a case of hardware failure, or some other
resource problem that freezes the OS, there is no built-in solution to migrate or
restart existing pods.

If the node misbehaves, and processes can not run anymore the control
plane will start counting down. It will either be the kubelet process which doesn't
report status to the control plane (see [node_status_update_frequency][]) or
the containers themselves will fail/crash and be marked as `phase: failed`.
Nodes status conditions, set by the node-controller in the control plane, will
reflect the current status and how long the node has been in that state.
For example, in the case where the node fails to update its status to the
masters the node condition will be set to `type:Ready status:Unknown`.

In order to gain the workload back, reschedule it and start it all over, the control plane
needs to know that the the workload's pod is not running anymore. There are two
strategies to accomplish that:

- [`OutOfServiceTaint`][] - new core Kubernetes feature named [Non-Graceful Node
  Shutdown], it triggers pods on the node to be forcefully deleted if there are no
  matching tolerations on the pods. Persistent volumes attached to the shutdown node will
  be detached, and new pods will be created on a different running node. This
  is the recommended strategy.

- `ResourceDeletion` - it deletes the pods on the node. This strategy is still supported for
  backward compatibility with clusters running Kubernetes versions that do not support Non-Graceful
  Node Shutdown feature, but it is discouraged.

# Pod recovery flow

After the node is deleted, a pod is scheduled for deletion by the control
plane. Then, depending on deployment kind, a new pod with the same spec
will be created.

# Volume recovery flow

Regular volumes attached to pod are ephemeral and don't contain persisted data.
They are mostly used to mount secrets, config maps, share unix sockets between
components and maybe temporary storage of data. Recovering them is not considered
an issue.
Persistent volumes however are the main concern of workload that is lost.
For persistent volumes from a CSI driver, the spec defines that a deletion pod
will trigger the deletion of `VolumeAttachment`, which will trigger unmounting
the volume from the underlying storage system - a unique operation per driver provider.
After a successful unpublishing the pod and the volume can start again, on a different
node.

## Virtualized worker node

Nodes which are VMs should be configured with a watchdog device (see [libvirt's watchdog support][])
In case it's not configured then self-node-remediation fallbacks to rebooting the machine
using 'systemctl reboot'. The benefits of a virtualized watchdog is that its running
on the hypervisor and is not vulnerable to resource starvation problem in the VM level
resulting a quicker reboot action.

# Statefulset recovery flow

TBD

[node_status_update_frequency]: https://kubernetes.io/docs/reference/command-line-tools-reference/kubelet/
[`OutOfServiceTaint`]: https://kubernetes.io/docs/reference/labels-annotations-taints/#node-kubernetes-io-out-of-service
[Non-Graceful Node Shutdown]: https://kubernetes.io/blog/2023/08/16/kubernetes-1-28-non-graceful-node-shutdown-ga/
[libvirt's watchdog support]: https://libvirt.org/formatdomain.html#watchdog-device
