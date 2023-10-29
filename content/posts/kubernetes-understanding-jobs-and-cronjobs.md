---
title: "Kubernetes: Understanding Jobs and CronJobs"
date: 2023-05-10
tags: ["Kubernetes", "Jobs", "CronJobs", "Orchestration"]
categories: ["Kubernetes", "Containers", "Orchestration"]
draft: true
---

In Kubernetes, we often have pods that are meant to run indefinitely. However, there are scenarios where we need to run a specific task and exit, like a database migration. For these use cases, we use a Kubernetes resource called Job.

## Introduction to Jobs in Kubernetes

A Job in Kubernetes is a resource that, like a Deployment, creates one or more pods. It then monitors these pods to ensure they complete their tasks and exit successfully. Once all the pods finish their tasks, the Job is marked as completed.

Here's an example of a Job:

```yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: my-job
spec:
  template:
    spec:
      containers:
      - name: my-job
        image: my-image
        command: ['do', 'something']
      restartPolicy: OnFailure
```

This template is similar to a Deployment, with an addition of restartPolicy. This property defines when a pod should be restarted. The possible values are Always, OnFailure, and Never. A Job can't use Always, so we must choose between OnFailure and Never.

## Understanding Job Failure and Retries
Things can go wrong during a Job's execution, and a pod can fail due to application errors or node failure. When a pod fails, the Job will try to run it again, using an exponential back-off delay for retries. By default, a Job will retry a failed pod up to six times.

We can override this default using the backoffLimit property:

```
apiVersion: batch/v1
kind: Job
metadata:
  name: my-job
spec:
  backoffLimit: 10
  template:
    # ...
```

Additionally, we can set the activeDeadlineSeconds property to define how long a Job is allowed to run. After the specified number of seconds, if all the pods haven't finished successfully, the Job is considered to have failed.

## Scheduling Jobs with CronJobs
Kubernetes also has a high-level resource called CronJob for scheduling Jobs to run at specific times.

```
apiVersion: batch/v1beta1
kind: CronJob
metadata:
  name: my-cronjob
spec:
  schedule: "*/1 * * * *"
  jobTemplate:
    spec:
      template:
        spec:
          containers:
          - name: my-job
            image: my-image
            command: ['do', 'something']
          restartPolicy: OnFailure
```

The schedule property uses the crontab format, which allows us to specify when the Job should run.

## Recap
Jobs in Kubernetes are a powerful resource that lets us run specific tasks to completion, while CronJobs let us schedule these tasks. Both are essential tools when managing workloads in a Kubernetes environment.