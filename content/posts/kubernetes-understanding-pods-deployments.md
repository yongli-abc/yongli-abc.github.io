---
title: "Kubernetes: Understanding Pods, Deployments, and Probes"
date: 2023-05-08
draft: true
tags: ["Kubernetes", "Pods", "Deployments", "Probes"]
categories: ["Kubernetes", "Containers", "Orchestration"]
---

In this blog post, we'll explore some of the key concepts in Kubernetes, such as Pods, Deployments, and Probes. These concepts are crucial for understanding how Kubernetes manages and scales containerized applications efficiently.

## Pods

A Pod is the atomic unit of scheduling in Kubernetes and serves as the building block for running containers. Each Pod can contain one or more containers, and every time a container runs in Kubernetes, it runs inside a Pod.

When scaling applications, we create multiple Pods instead of creating a single Pod with multiple containers. Interactions with Pods are usually done through the `kubectl` command-line tool.

## Deployments

In Kubernetes, we rarely run Pods directly. Instead, we use Deployments to manage and control our Pods. Deployments provide several benefits:

- Automatic rescheduling of Pods when they die
- Scaling applications by increasing or decreasing the number of replicas
- Managing the rollout of new application versions without downtime
- Easy rollback of bad releases

## Rolling Updates

When releasing a new version of an application, Kubernetes uses a strategy called RollingUpdate by default. This strategy gradually replaces Pods running the old version with those running the new version. The rollout rate can be controlled using `maxSurge` and `maxUnavailable` properties.

There's also an alternative strategy called Recreate, which terminates all Pods running the old version before creating Pods with the new version. This strategy may result in downtime but ensures that different versions don't run simultaneously.

## Readiness and Liveness Probes

Kubernetes provides readinessProbe and livenessProbe to check the health of Pods. A readinessProbe ensures that a Pod is ready to accept traffic before it starts receiving requests. A livenessProbe, on the other hand, checks the health of a running Pod and restarts it if it's unhealthy.