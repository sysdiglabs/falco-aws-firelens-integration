# Multi-cluster security with Falco and FluentBit on Amazon EKS & ECS

This repository hold all source code needed for the blogpost about `Multi-cluster
security with Falco and FluentBit on Amazon EKS & ECS`

There are one directory per step or piece of infrastructure to automate:

* `eks`: Deploy Falco and FluentBit on EKS
* `ecs`: Deploy Falco and FluentBit on ECS
* `kinesis`: Create Kinesis streams to send alerts to ElasticSearch
