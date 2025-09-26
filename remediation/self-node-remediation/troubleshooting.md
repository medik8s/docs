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

In addition, check the logs of the self node remediation agents. You should check the logs of the pod on the unhealthy node, and of other pod on a healthy node.

If the following logs appear, it indicates that SNR failed to retrieve the list of worker nodes. This issue occurs because SNR uses the `node-role.kubernetes.io/worker` label as a selector when creating the peer list of worker nodes.

```
2024-11-14T03:34:40.012616124Z  INFO    api-check       failed to check api server: api server readyz endpoint error: Get "https://10.96.0.1:443/readyz?exclude=shutdown": context deadline exceeded
2024-11-14T03:34:40.01264309Z   INFO    api-check       Error count exceeds threshold, trying to ask other nodes if I'm healthy
2024-11-14T03:34:40.012646838Z  INFO    api-check       Peers list is empty and / or couldn't be retrieved from server, nothing we can do, so consider the node being healthy
2024-11-14T03:34:40.012649011Z  INFO    api-check       peers did not confirm that we are unhealthy, ignoring error
```

To resolve this, set node labels on your worker nodes by running the following command:

`kubectl label nodes <node-name> node-role.kubernetes.io/worker=`

For more details, see [issue #268](https://github.com/medik8s/self-node-remediation/issues/268).

## Self Node Remediation daemonset still exists after operator uninstall

This is a known issue, and you should manually delete the self node remediation config CR to get it deleted.

## Control plane node is rebooting even though it's healthy

If the control plane node reboots unexpectedly, check the logs of the `self-node-remediation` pod:

```
kubectl logs self-node-remediation-ds-<id>
```

If you see logs like below, you need to set up DNS resolution for the control plane node name.

```
ERROR   controlPlane.Manager    kubelet service is down {"node name": "master", "error": "Get \"https://master:10250/pods\": dial tcp: lookup master on 10.96.0.10:53: server misbehaving"}
INFO    rebooter        watchdog feeding has stopped, waiting for reboot to commence
```

* in this example, the control plane node name got by `kubectl get nodes` is `master`.

For setting up DNS resolution, you can use any method that works in your environment. For example, [hosts plugin](https://coredns.io/plugins/hosts/) of [CoreDNS](https://coredns.io/) can be used to set up the name resolution by adding an entry like below to the CoreDNS configmap.

```yaml
        hosts {
           192.168.0.10 master
           fallthrough
        }
```

For more details, see [issue #267](https://github.com/medik8s/self-node-remediation/issues/267).

## How do I get community support?

Feel free to reach out in our [Medik8s google group](https://groups.google.com/g/medik8s)



