**Table of Contents**
1. [Introduction](#introduction)
1. [Kubernetes Architecture](#kubernetes-architecture)
    1. Cluster Architecture
    2. ETCD in Kubernetes
    3. Kube-API Server
    4. Kube Controller Manager
    5. Kube Scheduler
    6. Kubelet
    7. Kube Proxy
1. [Core Concepts](#core-concepts)
    1. Pods
    2. ReplicaSets
    3. Deployments
    4. Namespaces
    5. Mutli-Container Pods
1. [Application Configuration](#application-configuration)
    1. Environment Variables
    2. ConfigMaps
    3. Secrets
1. [Application Observability](#application-observability)
    1. Readiness and Liveness Probes
    2. Container Logging
    3. Monitor and Debug Applications
1. [Pod Design](#pod-design)
    1. Labels, Selectors and Annotations
    2. Rolling Updates and Rollbacks
1. [Services and Networking](#services-and-networking)
    1. Services
    2. Services - ClusterIP
    3. Ingress Networking
1. [Storage and State](#storage-and-state)
    1. Volumes
    2. Persistent Volumes
    3. Persistent Volume Claims
    4. Storage Classes
    5. StatefulSets
1. [Application Packaging](#application-packaging)
    1. Helm
    2. Operators

## Introduction
The content for this week is based on the official [Certified Kubernetes Application Developer](https://github.com/cncf/curriculum/blob/master/CKAD_Curriculum_v1.22.pdf) curriculum. I am adding on top of it a few pieces around the general Kubernetes architecture that I believe are important to understand.

It is not essential that you can remember every single detail from this week, but understand general idea and how Kubernetes works.

OpenShift will make interacting with a lot of these concepts significantly easier.

## Cluster Architecture

## Application Design and Build

## Application Deployment

## Application Observability and Maintenance

## Application Environment, Configuration and Security

## Services and Networking