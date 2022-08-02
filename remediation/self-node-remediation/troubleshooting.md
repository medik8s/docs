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

## Self Node Remediation daemonset still exists after operator uninstall
This is a known issue, and you should manually delete the self node remediation config CR to get it deleted.

## How do I get community support?
Feel free to reach out in our [medik8s google group](https://groups.google.com/g/medik8s)



