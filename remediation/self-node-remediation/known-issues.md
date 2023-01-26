---
layout: default
title: Known Issues
parent: Self Node Remediation
grand_parent: Remediation
nav_order: 4
---

# Known Issues
Self Node Remediation has several known issues:
1. Currently only one health detection system (e.g. NHC, MHC) is supported at the same time (i.e. you can't use NHC and MHC at the same time)
2. The timeout to assume the node has been rebooted is the same for all nodes. The safe timeout should be configured for the highest watchdog timeout
3. Uninstalling the operator doesn't remove the self node remediation daemonset. A user should delete the SelfNodeRemediationConfig CR to remove the daemonset
4. Upon installing self node remediation operator, it might take up to 2 minutes before the daemonset is deployed
5. IPv6 is not supported
6. At least two workers are required to get node fencing
7. At release 0.3 channel name was changed from "**alpha**" to "**stable**". This means that when releases prior to 0.3 are upgraded, the channel name needs to be changed manually
8. Prior to installing SNR on a Kubernetes 1.25+ cluster, a user must manually set a privileged PSA label (i.e. pod-security.kubernetes.io/enforce: privileged) on SNR's namespace. It gives SNR's agents permissions to reboot the node (in case it needs to be remediated).
