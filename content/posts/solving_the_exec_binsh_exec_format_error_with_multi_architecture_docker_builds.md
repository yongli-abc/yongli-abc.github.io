---
title: "Solving the 'exec /bin/sh: exec format error' with Multi-Architecture Docker Builds"
date: 2023-05-18
draft: false
description: "A guide on how to solve the 'exec format error' encountered when running Docker containers built for a different architecture."
tags: ["Docker", "Container", "Kubernetes"]
categories: ["Docker", "Container", "Kubernetes"]
---

## Introduction

In the world of containers and microservices, Docker is a popular tool for packaging applications along with their dependencies. However, when running Docker containers across different system architectures, you might encounter errors due to the mismatch in the architecture of the system where the Docker image was built and the system where the Docker container is being run.

One such error is `exec /bin/sh: exec format error`. In this blog post, we will explain the cause of this error and provide a solution.

## The Problem

Let's say you have built a Docker image on an `arm64` architecture system, and now you're trying to run a container from this image on an `amd64` architecture system. When doing this, you might encounter the following error:

```bash
exec /bin/sh: exec format error
```

This error occurs because the executable format of the system where the Docker image was built (`arm64`) is incompatible with the system where the Docker container is being run (`amd64`).

## The Solution: Multi-Architecture Docker Builds

Fortunately, Docker provides a solution to this problem: multi-architecture builds. With Docker Buildx, you can create Docker images that can run on different architectures.

To use Docker Buildx for building multi-architecture images, you first need to enable it:

```bash
docker buildx create --use
```

After enabling Docker Buildx, you can build a Docker image for multiple architectures. For example, to build an image that supports amd64 and arm64 architectures, you can use the following command:

```bash
docker buildx build --platform linux/amd64,linux/arm64 -t your-username/your-image:tag --push .
```

This command builds a Docker image for amd64 and arm64 architectures and pushes it to the Docker repository.

## Conclusion
The exec format error is a common issue that occurs when trying to run Docker containers across different system architectures. By using Docker Buildx for multi-architecture builds, you can ensure that your Docker images can run on different architectures without encountering this error.

This solution not only solves the exec format error but also makes your Docker images more portable and flexible, allowing them to run on a variety of systems and cloud services.