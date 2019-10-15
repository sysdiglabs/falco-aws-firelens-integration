# Multi-cluster security with Falco and FluentBit on Amazon EKS & ECS

This repository hold all source code needed for the blogpost about `Multi-cluster
security with Falco and FluentBit on Amazon EKS & ECS`

There are one directory per step or piece of infrastructure to automate:

* `ecs`: Deploy Falco and FluentBit on ECS
* `eks`: Deploy Falco and FluentBit on EKS

## Getting started

You will need the following requisites:

* `Helm` with Tiller deployed on the EKS cluster
* `aws cli` tools to handle all AWS configuration settings. Ensure you are using
  an aws cli tools which uses boto greater or equal to 1.12.224
* `jq` to help with the scripts

### Deploying EKS integration

Ensure your worker nodes can send logs to CloudWatch. We automated this step with
the Makefile but you will need to edit and set the `NODE_ROLE_NAME` value to your
own settings. Then:

```
$ cd eks
$ make
```

This will create and attach the EKS-CloudWatchLogs policy to your node IAM role
to make sure you can send logs to CloudWatch and will deploy FluentBit daemonset
with the CloudWatch output plugin.

Finally it will also deploy Falco using the Helm Chart.

### Deploying ECS integration

Like EKS, we automated this step with a Makefile. You will need to edit and set
the `CLUSTER_ARN` and `NODE_ROLE_NAME` as well. Then:

```
$ cd ecs
$ make
```

And this will create and attach the ECS-CloudWatchLogs policy to your node IAM
role to ensure you can send logs to CloudWatch and will create a task which
deploys Falco on ECS with an attached sidecar container for FluentBit which
sends the logs to CloudWatch.
