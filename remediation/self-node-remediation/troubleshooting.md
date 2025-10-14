---
layout: default
title: Troubleshooting
parent: Self Node Remediation
grand_parent: Remediation
nav_order: 5
---

# Self Node Remediation Troubleshooting

The self node remediation operator has one deployment for the operator, which installs a daemonset named `self-node-remediation-ds`.
The Daemonset is expected to run on all worker nodes.

After installation, `kubectl get ds self-node-remediation-ds -n <namespace>` should show the Daemonset status, and there should be an additional pod for the operator itself, on the same namespace.

The operator pod is responsible for syncing and creating the daemonset whenever the default self node remediation config CR changes, creating shared resources like certificates etc.

## Operator is installed but I don't see the daemonset

Please check the logs of the operator

## An unhealthy node was not remediated

First, you should check if SelfNodeRemediation (SNR) CR was created, this can be checked using `kubectl get ppr -A`.
If there wasn't SNR CR when the node turned unhealthy, you should probably check the logs of the health detection system (e.g. NHC) to understand why it wasn't created.

If SNR CR was created, make sure its name matches the unhealthy node/machine object.

If the node is still not being remediated after confirming the CR exists, verify that your worker nodes have the required `node-role.kubernetes.io/worker` label. SelfNodeRemediation uses this label as a selector to identify worker nodes and form a peer list for health determination.

Check if your nodes have this label:

```bash
kubectl get nodes -l node-role.kubernetes.io/worker --show-labels
```

If no nodes are listed, it indicates that the worker nodes lack the necessary label.
To resolve this, set node labels on your worker nodes by running the following command:

`kubectl label nodes <node-name> node-role.kubernetes.io/worker=`

For more details, see [issue #268](https://github.com/medik8s/self-node-remediation/issues/268).

In addition, check the logs of the self node remediation agents. You should check the logs of the pod on the unhealthy node, and of other pod on a healthy node.

## Self Node Remediation daemonset still exists after operator uninstall

This is a known issue, and you should manually delete the self node remediation config CR to get it deleted.

## Control plane node is rebooting even though it's healthy

If the control plane node reboots unexpectedly, check the logs of the `self-node-remediation` pod:

```
kubectl logs self-node-remediation-ds-<id>
```

If you see logs like below, you might need to set up DNS resolution for the control plane node name.

```
ERROR   controlPlane.Manager    kubelet service is down {"node name": "master", "error": "Get \"https://master:10250/pods\": dial tcp: lookup master on 10.96.0.10:53: server misbehaving"}
INFO    rebooter        watchdog feeding has stopped, waiting for reboot to commence
```

SNR requires DNS resolution for Kubernetes node names to function correctly. To diagnose this issue, check if your cluster's DNS can resolve the node names returned by `kubectl get nodes`. If DNS resolution is missing or misconfigured, you'll need to set up proper DNS resolution in your environment.

For more details, see [issue #267](https://github.com/medik8s/self-node-remediation/issues/267).

## How do I get community support?

Feel free to reach out in our [Medik8s google group](https://groups.google.com/g/medik8s)



