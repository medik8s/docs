---
layout: default
title: Getting Started
nav_order: 2
---

# Install
Installation is easy and takes few minutes to get up and running.

## Install on K8S or OKD
Go to [NHC in Operatorhub](https://operatorhub.io/operator/node-healthcheck-operator) and click "Install". Follow the instructions.

## Install on Openshift Container Platform
In the OCP UI console, go to Operators > OperatorHub and search for `Node Health Check` and click `Install`.
After few minutes, poison-pill will be automatically installed.

<video controls="true" allowfullscreen="true" width="640" height="480">
    <source src="/images/installation.mp4" type="video/mp4">
</video>

## Custom Configuration
Node Healthcheck Operator includes a dependancy on [Poison Pill](/PoisonPill) so that and opinitated defaults to be able to function right after installation.
You may want to tweak the configuration of both, or install one of the [alternatives to Poison Pill](/remediation/#implementations) in order to match your cluster needs.

To tweak NHC configuration see [NHC's README](https://github.com/medik8s/node-healthcheck-operator/blob/master/docs/README.md)
To change the default Poison Pill configuration, see [Poison Pill Configuration](/remediation/poison-pill/configuration/) page
