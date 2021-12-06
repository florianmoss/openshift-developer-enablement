**Table of Contents**
1. [Introduction](#introduction)
1. [Kubernetes Architecture](#kubernetes-architecture)
    1. [Cluster Architecture](#cluster-architecture)
    2. [ETCD in Kubernetes](#etcd-in-kubernetes)
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