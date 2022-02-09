---
layout: default
title: Known Issues
parent: Poison Pill
grand_parent: Remediation
nav_order: 4
---

# Known Issues
Poison Pill has several known issues:
1. Currently only one health detection system (e.g. NHC, MHC) is supported at the same time (i.e. you can't use NHC and MHC at the same time)
2. The timeout to assume the node has been rebooted is the same for all nodes. The safe timeout should be configured for the highest watchdog timeout
3. Poison Pill does not run on masters
4. Uninstalling the operator doesn't remove the poison pill daemonset. a user should delete the PoisonPillConfig CR to remove the daemonset
5. Upon poison pill installation, it might take up to 2 minutes before the daemonset is deployed
6. IPv6 is not supported
7. Clusters with OVN network plugin are not supported due to [Bug 1973286](https://bugzilla.redhat.com/show_bug.cgi?id=1973286)
8. At least two workers are required to get node fencing
9. At release 0.3 channel name was changed from "**alpha**" to "**stable**". This means that when releases prior to 0.3 are upgraded, the channel name needs to be changed manually 