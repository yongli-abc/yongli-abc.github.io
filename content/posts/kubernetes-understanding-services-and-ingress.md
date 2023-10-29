---
title: "Kubernetes: Understanding Services and Ingress"
date: 2023-05-08
draft: true
tags: ["Kubernetes", "Services", "Ingress"]
categories: ["Kubernetes"]
---

## Introduction to Kubernetes Services

In Kubernetes, Pods are ephemeral and can be terminated and created dynamically. To provide a stable network endpoint for Pods, we use a Kubernetes resource called a Service. Services enable communication between applications within the cluster and expose them to external users.

### ClusterIP

The simplest and default type of Service is ClusterIP. It allows communication between Pods running inside the cluster. For instance, if application *app-a* has three replicas and *app-b* requires a stable endpoint to access these replicas, we can create a ClusterIP Service for *app-a*.

### NodePort

NodePort is another type of Service that builds on top of ClusterIP. It opens a port on all worker nodes in the cluster and redirects incoming requests to the appropriate Pods, even if they are running on different nodes. NodePort Services are useful for exposing applications to the outside world.

### LoadBalancer

LoadBalancer is an extension of NodePort and ClusterIP Services. It provisions a Load Balancer on the cloud provider running the Kubernetes cluster. For example, if the cluster is on AWS, creating a LoadBalancer Service automatically creates an Elastic Load Balancer (ELB). This Service type is suitable for easily exposing applications to external traffic.

### ExternalName

Unlike other Service types, ExternalName provides a stable endpoint for an external service. For example, if you have a database running at *my-db.company.com*, you can create an ExternalName Service that points to this external address.

## Introduction to Ingress

Ingress is a Kubernetes resource that routes HTTP traffic to Services based on defined rules. It is not a Service type but acts as a smart router. An Ingress can manage traffic for multiple Services, while a LoadBalancer creates a separate load balancer for each Service.

Using Ingress has several advantages:

- Ingress allows you to route traffic to different Services with a single load balancer, reducing costs.
- Ingress can route requests to different paths, such as *example.com/foo* to the *foo* Service and *example.com/bar* to the *bar* Service.

In summary, a LoadBalancer is an easy way to expose Services, while an Ingress is more powerful and flexible.

## Recap

- Services provide a stable endpoint for Pods in Kubernetes, enabling communication within the cluster and exposure to external users.
- There are four types of Services: ClusterIP, NodePort, LoadBalancer, and ExternalName.
- Ingress is a Kubernetes resource that routes HTTP traffic to Services based on defined rules. It offers more flexibility than using LoadBalancer Services for traffic management.