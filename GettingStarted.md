# Getting Started
Installation is easy and takes few minutes to get up and running.

## Install on K8S or OKD
Go to https://operatorhub.io/operator/node-healthcheck-operator and click "Install". Follow the instructions.

## Install on Openshift Container Platform
In the OCP UI console, go to Operators > OperatorHub and search for "Node Health Check" and click "install".
After few minutes, poison-pill will be automatically installed.

## Custom Configuration
Node Healthcheck Operator and Poison Pill come with opinitated defaults to be able to function right after installation.
You may want to tweak the configuration to match your cluster needs.

To tweak NHC configuration see [NHC's README](https://github.com/medik8s/node-healthcheck-operator/blob/master/docs/README.md)
