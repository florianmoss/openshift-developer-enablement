**Table of Contents**
1. [Introduction](#introduction)
    1. [YAML](#yaml)
1. [Kubernetes Architecture](#kubernetes-architecture)
    1. [Cluster Architecture](#cluster-architecture)
    2. [etcd in Kubernetes](#etcd-in-kubernetes)
    3. [Kube-API Server](#kube-api-server)
    4. [Kube Controller Manager](#kube-controller-manager)
    5. [Kube Scheduler](#kube-scheduler)
    6. [Kubelet](#kubelet)
    7. [Kube Proxy](#kube-proxy)
1. [Core Concepts](#core-concepts)
    1. [Kubernetes Objects](#kubernetes-objects)
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

### YAML
Love it or hate it - you better make piece with the fact that you are gonna see more YAML files than you will see your children.

If you don't know how to use YAML, you better learn it now. Learn it properly once, it's worth it and it shouldn't take more than 30 minutes. 

Everything in Kubernetes is expressed in YAML files.

[CloudBess - Getting started with YAML](https://www.cloudbees.com/blog/yaml-tutorial-everything-you-need-get-started)

[YAML: Learn in X minutes](https://learnxinyminutes.com/docs/yaml/)
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
Kubernetes is fully API driven. The kube-api server is the 'frontend' for the control plane. Think about it as the gate into the harbor. 

The great thing is that you can have more than one gate. If you have more requests for your harbor, just create another gate and balance incoming traffic between the gates.

Most harbors have 3 gates ;)

### Kube Controller Manager
The kube controller manager is actually not one manager but has many managers. Each manager has a partcular job and runs in a loop. At every loop the manager makes sure that their specific area of the harbor is in order and exactly in the way the file system (etcd) tells them to. 

Our managers are really important, because they make sure things are exactly in the state we want them to be at!

### Kube Scheduler
The kube-scheduler is the crane master of the harbor. One ship might look already pretty busy? The crane master will then make sure to load another ship with the next container.

Loading containers is an ongoing tasks. Sometimes it is windy and a container goes over board, then the kube-scheduler needs to reassign a container with the exact same specifications.

### Kubelet
The kubelet is an agent on each of our ships (worker nodes) and makes sure that each pod (1 or more containers) are functioning as expected.

As developers we don't really care about this of course because all we want to do is fill containers with valuable content!

### Kube Proxy
Ok, I am running out of metaphors here! The kube-proxy is a network proxy that runs on each node in the cluster, it is responsible for implementing and adhering to network rules. It also is resposible for handling traffic into the pod.

## Core Concepts

### Kubernetes Objects
Everything in Kubernetes is expressed in YAML and is nothing but an object. 

Kubernetes objects are persistent entities in the Kubernetes system. Kubernetes uses these entities to represent the state of your cluster. Specifically, they can describe:

- What containerized applications are running (and on which nodes)
- The resources available to those applications
- The policies around how those applications behave, such as restart policies, upgrades, and fault-tolerance

A Kubernetes object is a "record of intent"--once you create the object, the Kubernetes system will constantly work to ensure that object exists. By creating an object, you're effectively telling the Kubernetes system what you want your cluster's workload to look like; this is your cluster's desired state.

To work with Kubernetes objects--whether to ```create```, ```modify```, or ```delete``` them--you'll need to use the Kubernetes API. When you use the kubectl command-line interface, for example, the CLI makes the necessary Kubernetes API calls for you. You can also use the Kubernetes API directly in your own programs using one of the Client Libraries.

In the .yaml file for the Kubernetes object you want to create, you'll need to set values for the following fields:

- ```apiVersion``` - Which version of the Kubernetes API you're using to create this object
- ```kind``` - What kind of object you want to create
- ```metadata``` - Data that helps uniquely identify the object, including a name string, UID, and optional namespace
- ```spec``` - What state you desire for the object

The precise format of the object spec is different for every Kubernetes object, and contains nested fields specific to that object. 

```yaml
# The api version is usually something like v1, v2, or apps/v1
apiVersion: apps/v1
# There are various kinds of objects, Deployment is one of them
kind: Deployment
# This is where we can use labels and names to group/order our objects
metadata:
  name: nginx-deployment
# This is the 'body' of our object and specifies what its behaviour
spec:
  selector:
    matchLabels:
      app: nginx
  replicas: 2 # tells deployment to run 2 pods matching the template
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```

If you knew nothing about the ```Deployment``` object and its content, the [Kubernetes Docs](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) will be able to help you.

[More on Kubernetes Objects](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/)
### Pods
A Pod is a set of running containers in a cluster. This means: One or more.

Like individual application containers, Pods are considered to be relatively ephemeral (rather than durable) entities. Pods are created, assigned a unique ID (UID), and scheduled to nodes where they remain until termination (according to restart policy) or deletion. If a Node dies, the Pods scheduled to that node are scheduled for deletion after a timeout period.

Pods do not, by themselves, self-heal. If a Pod is scheduled to a node that then fails, the Pod is deleted; likewise, a Pod won't survive an eviction due to a lack of resources or Node maintenance. Kubernetes uses a higher-level abstraction, called a controller, that handles the work of managing the relatively disposable Pod instances.

As mentioned earlier, a Pod is expressed in YAML:



[Pods: Kubernetes Docs](https://kubernetes.io/docs/concepts/workloads/pods/)

### ReplicaSets

### Deployments

### Namespaces

### Mutli-Container Pods

## Application Configuration

### Environment Variables

### ConfigMaps

### Secrets

## Application Observability

### Readiness and Liveness Probes

### Container Logging

### Monitor and Debug Applications

## Pod Design

### Labels, Selectors and Annotations

### Rolling Updates and Rollbacks

## Services and Networking

### Services

### Services - ClusterIP

### Ingress Networking

## Storage and State

### Volumes

### Persistent Volumes

### Persistent Volume Claims

### Storage Classes

### StatefulSets

## Application Packaging

### Helm

### Operators

## Additional References

### Kubernetes Docs
[kubernetes.io](https://kubernetes.io/docs/home/)

### Kube by Example
[kube by:example](https://kubebyexample.com/)