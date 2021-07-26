---
layout: default
title: Troubleshooting
parent: Poison Pill
grand_parent: Isolating Nodes
nav_order: 4
---

# Poison Pill Troubleshooting

The poison pill operator has one deployment for the operator, which installs a daemonset named `poison-pill-ds`.
The Daemonset is expected to run on all worker nodes.

After installation, `kubectl get ds poison-pill-ds -n <namespace>` should show the Daemonset status, and there should be an additional pod for the operator itself, on the same namespace.

The operator pod is responsible for syncing and creating the daemonset whenever the default poison pill config CR changes, creating shared resources like certificates etc.

## Operator is installed but I don't see the daemonset
Please check the logs of the operator

## An unheatlhy node was not remediated
First you should check if PoisonPillRemediation (ppr) cr was created, this can be checked using `kubectl get ppr -A`.
If there wasn't PPR CR when the node turned unhealthy, you should probably check the logs of the health detection system (e.g. NHC) to understand why it wasn't created.

If ppr CR was created, make sure its name matches the unhealthy node/machine object.

In addition, check the logs of the poison pill agents. You should check the logs of the pod on the unhealthy node, and of other pod on a healthy node.

## Poison Pill daemonset still exists after operator uninstall
This is a known issue, and you should manually delete the poison pill config CR to get it deleted.

## How do I get community support?
Feel free to reach out in our [medik8s google group](https://groups.google.com/g/medik8s)



