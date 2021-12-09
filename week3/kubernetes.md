**Table of Contents**
1. [Introduction](#introduction)
1. [Kubernetes Architecture](#kubernetes-architecture)
    1. [Cluster Architecture](#cluster-architecture)
    2. [etcd in Kubernetes](#etcd-in-kubernetes)
    3. [Kube-API Server](#kube-api-server)
    4. [Kube Controller Manager](#kube-controller-manager)
    5. [Kube Scheduler](#kube-scheduler)
    6. [Kubelet](#kubelet)
    7. [Kube Proxy](#kube-proxy)
1. [Core Concepts](#core-concepts)
    1. [Pods](#pods)
    2. [ReplicaSets](#replicasets)
    3. [Deployments](#deployments)
    4. [Namespaces](#namespaces)
    5. [Mutli-Container Pods](#multi-container-pods)
1. [Application Configuration](#application-configuration)
    1. [Environment Variables](#environment-variables)
    2. [ConfigMaps](#config-maps)
    3. [Secrets](#secrets)
1. [Application Observability](#application-observability)
    1. [Readiness and Liveness Probes](#readiness-and-liveness-probes)
    2. [Container Logging](#container-logging)
    3. [Monitor and Debug Applications](#monitor-and-debug-applications)
1. [Pod Design](#pod-design)
    1. [Labels, Selectors and Annotations](#labels-selectors-and-annotations)
    2. [Rolling Updates and Rollbacks](#rolling-updates-and-rollbacks)
1. [Services and Networking](#services-and-networking)
    1. [Services](#services)
    2. [Services - ClusterIP](#services-clusterip)
    3. [Ingress Networking](#ingress-networking)
1. [Storage and State](#storage-and-state)
    1. [Volumes](#volumes)
    2. [Persistent Volumes](#persistent-volumes)
    3. [Persistent Volume Claims](#persisten-volume-claims)
    4. [Storage Classes](#storage-classes)
    5. [StatefulSets](#statefulsets)
1. [Application Packaging](#application-packaging)
    1. [Helm](#helm)
    2. [Operators](#operators)
1. [Additional References](#additional-references)

## Introduction
The content for this week is based on the official [Certified Kubernetes Application Developer](https://github.com/cncf/curriculum/blob/master/CKAD_Curriculum_v1.22.pdf) curriculum. I am adding on top of it a few pieces around the general Kubernetes architecture that I believe are important to understand.

It is not essential that you can remember every single detail from this week, but understand general idea and how Kubernetes works.

OpenShift will make interacting with a lot of these concepts significantly easier.

## Kubernetes Architecture
Kubernetes is a portable, extensible, open-source platform for managing containerized workloads and services, that facilitates both declarative configuration and automation.

Let's remember - we talked about containers in the last week. Containers itself are fairly primitive and are 'only' a way to package up an application. A container by itself is pretty useless when we think about easing the operations side of things.

![Container Deployments vs other ways](images/containers.png)

Containers are a good way to bundle and run your applications. In a production environment, you need to manage the containers that run the applications and ensure that there is no downtime. For example, if a container goes down, another container needs to start. Wouldn't it be easier if this behavior was handled by a system?

That's how Kubernetes comes to the rescue! Kubernetes provides you with a framework to run distributed systems resiliently. It takes care of scaling and failover for your application, provides deployment patterns, and more. For example, Kubernetes can easily manage a canary deployment for your system.

**Service discovery and load balancing**

Kubernetes can expose a container using the DNS name or using their own IP address. If traffic to a container is high, Kubernetes is able to load balance and distribute the network traffic so that the deployment is stable.

**Storage orchestration**

Kubernetes allows you to automatically mount a storage system of your choice, such as local storages, public cloud providers, and more.

**Automated rollouts and rollbacks** 

You can describe the desired state for your deployed containers using Kubernetes, and it can change the actual state to the desired state at a controlled rate. For example, you can automate Kubernetes to create new containers for your deployment, remove existing containers and adopt all their resources to the new container.

**Automatic bin packing** 

You provide Kubernetes with a cluster of nodes that it can use to run containerized tasks. You tell Kubernetes how much CPU and memory (RAM) each container needs. Kubernetes can fit containers onto your nodes to make the best use of your resources.

**Self-healing** 

Kubernetes restarts containers that fail, replaces containers, kills containers that don't respond to your user-defined health check, and doesn't advertise them to clients until they are ready to serve.

**Secret and configuration management** 

Kubernetes lets you store and manage sensitive information, such as passwords, OAuth tokens, and SSH keys. You can deploy and update secrets and application configuration without rebuilding your container images, and without exposing secrets in your stack configuration.


### Cluster Architecture
So what exactly is it and how does it look from an architecture perspective?

Like this..

![Kubernetes Architecture](images/kubernetes.png)

Source: [Ashish Patel](https://medium.com/devops-mojo/kubernetes-architecture-overview-introduction-to-k8s-architecture-and-understanding-k8s-cluster-components-90e11eb34ccd)

Ok, I admit that this is not straight forward at this stage. The important thing to understand at this stage is: There is a control plane side and a worker node side.

The control plane is responsible for the actual orchestration part. Think about it like a harbor where container ships are being loaded and unloaded.

The actual container ship are the worker nodes. These worker nodes carry/host your containers. 

The individual parts of the operation will be explained in more detail down below. At this stage, all you need to know:

control plane => harbor

worker nodes => container ships

containers => what the harbor orchestrates onto the container ships are containers, we will call them Pods though.

### etcd in Kubernetes
Think about etcd as the fileroom of the harbor. All information about incoming ships, outgoing ships, container deliveries etc need to be stored somewhere. 

This is what etcd is: A key-value store for all cluster data. 

### Kube-API Server

### Kube Controller Manager

### Kube Scheduler

### Kubelet

### Kube Proxy

## Core Concepts

#### Pods

#### ReplicaSets

#### Deployments

#### Namespaces

#### Mutli-Container Pods

## Application Configuration

#### Environment Variables

#### ConfigMaps

#### Secrets

## Application Observability

#### Readiness and Liveness Probes

#### Container Logging

#### Monitor and Debug Applications

## Pod Design

#### Labels, Selectors and Annotations

#### Rolling Updates and Rollbacks

## Services and Networking

#### Services

#### Services - ClusterIP

#### Ingress Networking

## Storage and State

#### Volumes

#### Persistent Volumes

#### Persistent Volume Claims

#### Storage Classes

#### StatefulSets

## Application Packaging

#### Helm

#### Operators

## Additional References

#### Kubernetes Docs
[kubernetes.io](https://kubernetes.io/docs/home/)

#### Kube by Example
[kube by:example](https://kubebyexample.com/)