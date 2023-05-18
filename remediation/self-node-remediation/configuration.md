---
layout: default
title: Configuration
parent: Self Node Remediation
grand_parent: Remediation
nav_order: 2
---

# Self Node Remediation Configuration
Self Node Remediation utilizes a custom resource (CR) to define a custom configuration.
The `SelfNodeRemediationConfig` CR is automatically created upon installation.
Currently there are two configuration fields:
1. safeTimeToAssumeNodeRebootedSeconds: 180 - Specify the timeout duration for the surviving peer, after which the Operator can assume that an unhealthy node has been rebooted. The Operator automatically calculates the lower limit for this value. However, if different nodes have different watchdog timeouts, you must change this value to a higher value.
2. watchdogFilePath: /dev/watchdog - Specify the file path of the watchdog device in the nodes. If you enter an incorrect path to the watchdog device, the Self Node Remediation Operator automatically detects the softdog device path.
   If a watchdog device is unavailable, the SelfNodeRemediationConfig CR uses a software reboot.
3. isSoftwareRebootEnabled: true - Specify if you want to enable software reboot of the unhealthy nodes. By default, the value of isSoftwareRebootEnabled is set to true. To disable the software reboot, set the parameter value to false.
4. apiServerTimeout: 15s - Specify the timeout duration to check connectivity with each API server. When this duration elapses, the Operator starts remediation. The timeout duration must be greater than or equal to 10 milliseconds.
5. apiCheckInterval: 5s - Specify the frequency to check connectivity with each API server. The timeout duration must be greater than or equal to 1 second.
6. maxApiErrorThreshold: 3 - Specify a threshold value. After reaching this threshold, the node starts contacting its peers. The threshold value must be greater than or equal to 1 second.
7. peerApiServerTimeout: 5s - Specify the duration of the timeout for the peer to connect the API server. The timeout duration must be greater than or equal to 10 milliseconds.
8. peerDialTimeout: 5s - Specify the duration of the timeout for establishing connection with the peer. The timeout duration must be greater than or equal to 10 milliseconds.
9. peerRequestTimeout: 5s - Specify the duration of the timeout to get a response from the peer. The timeout duration must be greater than or equal to 10 milliseconds.
10. peerUpdateInterval: 15m - Specify the frequency to update peer information, such as IP address. The timeout duration must be greater than or equal to 10 seconds.

The `SelfNodeRemediationConfig` CR will be created at the same namespace of the operator, with the name `self-node-remediation-config`.
A user may edit this CR but not create a new one.

Any change to the `SelfNodeRemediationConfig` CR will result in re-creation of the Self Node Remediation daemonset.
