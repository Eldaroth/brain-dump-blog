---
title: "Kubernetes Concepts"
subtitle: "Cloud Foundations"
date: 2023-01-03T17:58:47+01:00
tags: ['cloud','k8s']
draft: false
---
K8s (short for [Kubernetes](https://kubernetes.io/)) is an Open Source container orchestration tool originally developed by Google and handed over to the Cloud Native Computing Foundation (CNCF).

<!--more-->

The need for container orchestration tools arose due to a shift from Monolith applications to Microservices in recent years. The subsequent increased usage of containers (sometimes in the hundreds or thousands), and with it the necessaty to manage them over several environments, caused a need for orchestration technologies.

K8s helps managing containers, or rather containerized applications, of various sizes and numbers in different deployment environments (physical, virtual, cloud or any combination thereof).

The following is only a basic overview of the K8s architecture and by no means complete. The [Kubernetes Documentation](https://kubernetes.io/docs/concepts/) has more detailed explanations for each of the below described components.

### Features
* High availability, i.e. applications have no downtime as they are self-healing; K8s restarts containers that fail, replaces/kills containers that don't respond to pre-defined health checks etc.
* Scalability, i.e. high performance due to scaling (up or down) possbilities based on demand
* Disaster recovery, i.e. containerized applications can run from the latest state based on recovered data, e.g. after infrastructure problem arise (data loss, server issues etc.)

# Architecture
A K8s cluster is made up of at least
* 1 Master Node (usually up to 2 or more in a productive environment), running various important K8s processes like

	| Process | Description |
	|---------|-------------|
	| API Server | entrypoint to the cluster (like CLI, API or GUI (Dashboard))|
	| Controller Manager | keeps track of the happenings on the cluster (i.e. whether something needs to be repaired or a pod died and needs to be restarted) |
	| Scheduler | scheduling containers on different nodes based on the workload and available server ressources (i.e. decides on which node the next container should be scheduled on) |
	| etcd | Key-Value Storage; holds at any time the current state of the K8s cluster (configuration and status data of each node and container) - backups are usually made of an etcd snapshot |

* 1 .. n Worker Nodes (referred to as simply "nodes") - each node has a **kubelet** process running on it, which makes it possible for the cluster nodes to talk to each other and execute tasks on them (like running application processes). Depending on the distribution of the work load, various numbers of containers are running on the worker nodes.

* Virtual Network - spans over all nodes in the cluster and enables the nodes to talk to each other; creates one "unified machine"

The master node is much more important than the worker nodes, as it is key in managing the K8s cluster. In productive environments there are usually multiple master nodes (2 or more). So if one master node is down, the cluster continous to function smoothly because there are other master nodes available.

# Components
Basic Components in the Kubernetes environment consist of elements like Pods, Deployments or Services.

## Node
Worker node; a simple server (physical or virtual machine). Each Node is managed by the Control Plane and includes the kubelet process, the container runtime and a network proxy (kube-proxy).

## Pod
The most basic and **smallest** deployable unit in Kubernetes. A pod is an **abstraction** over a container (e.g. Docker or other container runtimes like Podman or cri-o, also see [CNCF Blog - Demystifying containers – part II: container runtimes](https://www.cncf.io/blog/2019/07/15/demystifying-containers-part-ii-container-runtimes/)). A Pod creates a running environment, i.e. a layer on top of a container, as K8s wants to abstract away the container runtime/technology so you can use any container technology you would like.

In a microservice environment, usually one application is run per Pod. But Kubernetes also allows to run multiple application in one pod.

Each Pod gets its **own IP address**; the pods can communicate with each other over this IP (internal IP). But as Pods are ephemeral - they can "die" very easily; i.e. if a DB Pod has crashed, a new DB will be created with a **new IP address** - which is inconvenient if applications require to communicate with the DB pod. This is why K8s knows another component called Service.

## Service
Basically its a **permanent IP address** which can be attached to a pod. The advantage is that the lifecycles of the Pod and Service are not linked, i.e. if the pod dies, the Service continous to exist and the IP address stays the same.

There are several **types** of Services, like internal or external Services. External services open the communication from external sources, for example if you would like to allow access to your app from a browser. However, the external Service address usually is not as practicle, as it consists of an internal IP address and port - which is fine for testing. For external us there is another component called **Ingress**.

The Service also acts as a load balancer between the replicas within the same Deployment.

### Ingress
Ingress is on "top" of a Service, so if a request is made to the application, if first comes to the Ingress and is then forwarded to the external Service (routes traffic into the cluster).

## ConfigMap
Pods communicate using a Service, e.g. if the application communicates with a DB. But how do we configure the DB endpoint with which the application has to communicate? One way would be to configure the endpoint directly in the application configuration. However, if something changes with the endpoint (e.g. the DB pod crushes and the new pod receives a new internal IP) we would have to adjust the application configuration, re-build and deploy the application anew and re-start the application pod.

Therefore K8s has the ConfigMap component, which is an external configruation for your application. It usually contains URLs for DBs or login data like username or password in the form of environmental variables. The varialbes are defined by the container, so looking at the container documentation tells you which variables are available or required.

For sensitive data like usernames or passwords, there is another K8s component better suited for it - Secrets.

## Secret
Used to store sensitive/secret data. Secrets are stored in Base64 encoding - which does not automatically make it secure. But there are 3rd party tools which allow you to encrypt Secrets, like [Kubeseal](https://github.com/bitnami-labs/sealed-secrets) (SealedSecrets) by Bitnami.

Pods can read Secrets data like they do from the ConfigMap.

## Volumes (Data Storage)
Volumes attach physical storage on a hard drive to the pod. The storage can be on a local machine (same server like the node) or on remote storage (outside K8s cluster). Volumes are separated from the K8s cluster and are not impacted by any restarts or crashes of the pods.

Important: K8s clusters do not manage any data persistence, i.e. storage has to be managed separated from the K8s setup.

## Deployment
Basically a **Blueprint**, another abstraction layer on top of Pods. Within the Deployment you specify how many replicas of a specific Pod you would like to have run.

**Important:** The replicas are connected to the same Service, i.e. if one of the replicas dies, the Service (acting as a Load Balancer) will forward the request to another Pod replica.

### StatefulSet
Services requiring a "state", like a DB, cannot simply be replicated like any other application. For stateful apps/databases, K8s know the StatefulSet. As working with StatefulSets is not as simple as working with Deployments, DBs are often hosted outside of the K8s cluster.

***
### Sources
* [Kubernetes Crash Course for Absolute Beginners - TechWorld with Nana [YouTube Video]](https://www.youtube.com/watch?v=s_o8dwzRlu4&list=PL0bJVjzUjenVRIikbhHZjXOMSCGvqb1oU&index=5)
* [Kubernetes Documentation - Concepts](https://kubernetes.io/docs/concepts/)
* [CNCF Blog - Demystifying containers – part II: container runtimes](https://www.cncf.io/blog/2019/07/15/demystifying-containers-part-ii-container-runtimes/)