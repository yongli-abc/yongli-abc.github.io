---
title: "Understanding Kubernetes Watch Mechanism, HTTP Long Polling, and Chunked Transfer Encoding"
date: 2023-05-22
draft: true
categories: ["Kubernetes", "Networking"]
tags: ["Kubernetes", "API Server", "HTTP Long Polling", "TCP", "Controllers", "Chunked Transfer Encoding"]
---

Kubernetes (K8s) is an open-source platform for managing containerized workloads and services. One of the core concepts of Kubernetes is the "watch" mechanism used by its controllers. In this post, we'll delve into how this mechanism works, along with a discussion of HTTP long polling and chunked transfer encoding.

## Kubernetes Watch Mechanism

In Kubernetes, a controller watches for changes to resources using a pattern called "level-based" rather than "edge-based". This means that the controller doesn't rely on being directly informed about each change by the API Server. Instead, it constantly watches the state of the system and reacts to the current state, as opposed to specific events.

The controller achieves this using the "watch" API in Kubernetes. This involves the controller establishing a long-lived connection with the API server and receiving updates as they happen. When a resource (like a Deployment or a ReplicaSet) is created, updated, or deleted, the API server sends an update to the relevant controller over the watch stream. The controller, upon receiving an update, compares the actual state of the system with the desired state. If there's a discrepancy, it takes action to reconcile the two.

This watch mechanism is used by all Kubernetes controllers, following a common pattern often referred to as the "controller pattern" or the "reconciler pattern".

## HTTP Long Polling and Chunked Transfer Encoding

The watch functionality in Kubernetes is implemented using HTTP long polling, in conjunction with HTTP chunked transfer encoding. When a client initiates a watch request, it's essentially an HTTP GET request to the Kubernetes API server with a `watch=true` parameter in the query string. 

The server processes the request and keeps the connection open, sending updates to the client whenever the state of the watched resources changes. These updates are sent as chunks of data over the same HTTP response. This is possible because of the chunked transfer encoding feature of HTTP/1.1, which allows the server to send the response in chunks as data becomes available, rather than having to send it all at once. This mechanism is efficient and well-suited to situations like this where the server needs to keep the client updated about changes as they happen.

## TCP Connections

HTTP, whether it's traditional short-lived HTTP or long-polling HTTP, is a protocol that is layered on top of TCP/IP. When a client, such as a Kubernetes controller, opens a TCP connection to the API server and sends an HTTP GET request over this connection, the server accepts the TCP connection and processes the HTTP request. It keeps the connection open and uses it to send updates to the client whenever there's a change to the watched resources.

It's worth noting that in a real-world Kubernetes deployment, these connections would typically be secured using TLS (Transport Layer Security), which provides encryption and authentication on top of the underlying TCP connection.

In summary, Kubernetes leverages the power of HTTP long polling and chunked transfer encoding to implement an efficient and robust system for watching changes in resources, enabling it to maintain the desired state of the system.
