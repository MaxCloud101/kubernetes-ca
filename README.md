# Introduction to kubernetes

- CA course: https://cloudacademy.com/course/introduction-to-kubernetes
- GitHub: https://github.com/cloudacademy/intro-to-k8s/tree/master/src

## 1 Course Introduction

### 1.1 Introduction

Kubernetes is a production-grade container orchestation system that helps you maximize the benefits of using containers.

## 2 Overview of kubernetes

### 2.1 Kubernetes overview

What is kuberenetes?      

- Open-source container orchestration tool designed to automate, deploying, scaling, and operating containerized applications
- Born out of Google's experience running production workloads at scale
- Allows organizations to increase their velocity by releasing and recovering faster

More about kubernetes

- Kubernetes is a distributed system
- Machines may be physical, virtual, on-prem, or in the cloud
- Schedules containers on machines, 
- Moves containers as machines are added/removed
- Can use different container runtimes
- Modular, extensible desing

Using kubernetes

- Declarative configuration
- Deploy containers
- Wire up networking
- Scale and expose services

Kubernetes operation

- Automatically recover from machine failures
- Built-in support for machine maintenance
- Join clusters with federation

Kubernetes features highlights

- Automated deployment rollout and rollback
- Seamless horizontal scaling
- Secret management
- Service discovery and load balancing
- Linux and windows container support
- Simple log collection
- Role-based access control
- Batch job processing
- CPU and memory quotas
- Persistent volume management
- Stateful application support

Container orchestraion landscape

- There has been a surge in tools to support enterprises adopting containers in production
- We will compare Kubernetes with other tools to get a better undestanding
- Compare to: DCOS, Amazon ECS, and Docker swarm mode

### 2.2 Deploying kubernetes

Single-node kubernetes cluster

- Docker Desktop for Mac and Windows
- Minikube
- Kubeadm

Single node kubernetes clusters for continous integration

- Create ephemeral clusters that start quickly and are in a pristine state for testing applications in kubernetes
- Kubernetes-in-Docker (kind) is made especifically for this use case https://github.com/kubernetes-sigs/kind

Multi-node kubernetes cluster

- For your production workloads
- Horizontal scaling
- Tolerate node failures
- Ask several key questions to decide which solution is best

Fully-managed

- Amazon EKS
- AKS (Azure)
- GKE (Google cloud)

### 2.3 Kubernetes architecture

A word about kubernetes terminology

- Kuberenetes introduces its own dialect to the orchestation space
- Understanding the terminology important part of success with kubernetes
- We will define terms as they arise and the kubernetes glossary is available for reference

Kubernetes architecture

- Cluster refers to all of the machines collectively and can be throught of as the entire running system 
- Nodes are machines in the cluster
- Nodes are categorized as workers or masters
- Worker nodes include software to run containers managed by the kubernetes control plane
- The control plane is a set of APIs and software that Kubernetes users interact with
- The APIs and sofware are referred to as master components

Scheduling

- Control plane schedules containers onto nodes
- Scheduling descicions consider required CPU and other factors
- Scheduling refers to the desicion process of placing containers onto node

Kubernetes pods

- Groups of containers
- Pods are the smallest building blocks in kubernetes
- More complex and useful abstractions built on top of pods

Kubernetes services

- Services define networking rules for exposing group of pods
  - To other pods
  - To the public internet

Kubernetes deployments

- Manage deploying configuration changes to running pods
- Horizontal scaling

### 2.4 Interacting with kubernetes

The kubernetes API server

- Modify cluster state information by sending requests to the kubernetes API server
- The API server is a master component that acs as the frontend for the cluster

Interacting with kubernetes: Method 1 - REST API

- It is possible but not common to work directly with the API server
- You might need to if there is no Kubernetes Client Library for your programming language

Interacting with kubernetes: Method 2 - CLIENT LIBRARIES

- Handles authenticating and managing individual REST API request and responses
- Kubernetes maintains official client libraries
- Community-maintained librarie when no official library exists

Interacting with kubernetes: Method 3 - KUBECTL

- Issue high-level commands that are translated into REST API calls
- Works with local and remote clusters

Kubectl

- kubernetes success correlates with kubectl skill
- Manages all differents types of Kubernetes resources, and provides debugging and introspection features
- Kubectl commands follow an easy to understand pattern

Interacting with kubernetes: Method 4 - WEB DASHBOARD

## Deploying containerized applications to kubernetes

### 3.1 Pods

What are pods

- Basic building block in kubernetes
- One or more containers in a pod
- Pod containers all share a container network
- One IP address per pod

Whats's in a pod declaration?

- Container image
- Container ports
- Container restart policy
- Resource limits

Why use manifests?

- Can check into source control
- Easy to share
- Easier to work with

Example: Create simple pod

1.1-basic_pod.yaml

Example: Create simple pod with port

1.2-port_pod.yaml

Example: Create labeled pod

1.2-labeled_pod.yaml

Best Quality of Server

Kubernetes provides different levels of Quality of Service to pods depending on what they request and what limits are set for them.

Pods that need to stay up and consistently good can request guaranteed resources, while pods with less exacting requirements can use resources with less/no guarantee.

- Guaranteed (QoS): Pods are considered top-priority and are guaranteed to not be killed until they exceed their limits.
- Burstable (QoS): resources when available. Under system memory pressure, these containers are more likely to be killed once they exceed their requests and no Best-Effort pods exist.
- Best-Effort (QoS): Pods will be treated as lowest priority. Processes in these pods are the first to get killed if the system runs out of memory. These containers can use any amount of free memory in the node though.

Example: Create resources pod

1.4-resources_pod.yaml

### 3.2 Services

- A service defines networking rules for accessing Pods in the cluster and from the internet
- Use labels to select a group of pods
- Service has a fixed ip address
- Distribute requests across Pods in the group

Example: Create a service

2.1-web_service.yaml

- To verify node ips
```
kubectl describe nodes | grep -i address -A
```
### 3.3 Multi-container pods

Kubernetes namespaces

- Namespaces separate resources according to users, environments or applications
- Role-base access control (RBAC) to secure access per Namespace
- Using namespace is a best practice

Example: Create namespace

3.1-namespace.yaml

Example: Create a multi-container pod

3.2-multi_container.yaml

To see a log from specific container in pod

```
kubectl logs -n microservice app counter
```

To see logs in real time in specific container

```
kubectl logs -n microservice app poller -f
```

### 3.4 Service Discovery

Service discovery mechanisms

- Environment variables 
  - Service address automatically injected in containers
  - Environment variables follow namig conventions based on service name
- DNS
  - DNS records automatically created in cluster's DNS
  - Containers automatically configured to query cluster DNS

Example: Create a data tier pod

4.2-data_tier.yaml

Example: Create pod with service discovery with environment variables

4.3-app_tier.yaml

Example: Create pod with service discovery with DNS

4.4-support_tier.yaml

### 3.5 Deployments

- Represent multiple replicas of a pod
- Describe a desired state that kubernetes needs to achieve
- Deployment controller master component converges actual state to the desired state

Example: Create deployment

5.2-data_tier.yaml

5.3-app_tier.yaml

5.4-suppot_tier.yaml

### 3.6 AutoScaling

- Scale automatically base on CPU utilization (or custom metrics)
- Set target CPU along with min and max replicas
- Target CPU is expressed as a percentage of the Pod's CPU request

Metrics

- Autoscaling depends on metrics being collected
- Metrics server is one solution for collecting metrics
- Several manifest files are used to deploy Metrics server

https://github.com/kubernetes-sigs/metrics-server

Example: Create metrics server

```
kubectl create -f metrics-server/
```
To see pod resource utilization
```
watch kubectl top pods -n namespace
```

Example: Create deployment server

5.2-app_tier_cpu_request.yaml

Example: Create autoscaling

5.2-autoscale.yaml

To check pods createds in real time

```
watch -n 1 kubectl get -n namespace deployments app-tier
```
To see full list of shorthand notations, we can see here the horizontal pod autoscaler
```
kubectl api-resources
```
To describe hpa (horizontal pod autoscaler)
```
kubectl describe -n deployments hpa
```

### 3.7 Rollouts

- Rollouts update deployments
- Any change to a deployments template triggers a rollout
- Different rollout strategies are available

Rolling updates

- Default rollout strategy
- Update in groups rather than all-at-once
- Both old and new version running for some time
- Alternative is the recreate strategy
- Scaling is not a rollout
- kubectl has commands to check, pause, resume and rollback (undo) rollouts

### 3.8 Probes

Readiness probes

- Used to check when a Pod is ready to serve traffic/handle requests
- Useful after startup to check external dependencies
- Readiness probes set the Pod's ready condition. Services only send traffic to ready pods.

Liveness probes

- Detects when a pod enters a broken state
- Kubernetes will restart the pod for you
- Declare in the same way as readiness probes

Declaring probes

- Probes can be declared in a pod's containers
- All containers probes must pass for the pod to pass
- Probe actions can be a command that run in the container, an HTTP GET request, or opening a TCP socket

Example probes:

Data Tier (redis)

Liveness: open TCP socker

Readiness: redis-cli ping command

7.2-data_tier.yaml

App Tier (server)

Liveness: HTTP GET /prove/liveness

Readiness: HTTP GET /prove/readiness

7.3-app_tier.yaml

### 3.9 Init containers

- Sometimes you need to wait for a service, downloads, dynamic or desicions before starting a pod's containers
- Prefer to separate initialization wait logic from the container image
- Initialization is tightly coupled to the main application (belongs in the pod)
- Init containers allow you to run initialization tasks before starting the main containers

Init containers

- Pods can declare any number of init containers
- Init containers run in order and to completion
- Use their own images
- Easy way to block or delay starting an application
- Run every time a pod is created

Example: Wait for redis ready to connection before container creation

8.1-app_tier.yaml

### 3.10 volumes

- Sometimes useful to share data between containers in a Pod
- Lifetime of a container file system is limited to the container's lifetime
- Can lead to unexpected consequences if a container restarts

Pod storage in kubernetes

- Two high-level storage options: volumes and persistent volumes
- Used by mounting a directory in one or more containers in a pod
- Pods can use multiple volumes and persistent volumes
- Difference between volumes and persistent volumes is how their lifetime is managed

Volumes

- Volumes are tied to a pod and their lifecycle
- Share date between containers and tolerate container restarts
- Use for non-durable storage that is deleted with the pod
- Default volume type is emptyDir
- Data is lost if Pod is rescheduled on a different node

Persistent volumes

- Independent of Pod's lifetime
- Pods claim persistent volumes to use throughout their lifetime
- Can be mounted by multiple pods on different nodes if underlying storage supports it
- Can be provisioned statically in advance or dynamically on-demand

Persistent volume Claims

- Describe a pod's request for Persistent volume storage
- Includes how much storage, type of storage, and access mode
- Access mode can be read-write-one, read-only many, or read-write many
- PVC stays pending if no PV can satisfy it and dynamic provisioning is not enabled
- Connects to a pod throught a volume of type PVC

Storage volume types

- Wide variety of volume types to choose from
- Use persistent volumes for more durable storage types
- Suppot durable storage types include GCE Persistent disks, Azure disks, Amazon EBS, NFS, and iSCSI

Example: Create volumes

9.2-pv_data_tier.yaml

### 3.11 ConfigMaps and secrets

- Until now all container configuration has been in the pod spec
- This makes it less portable than it could be
- If sensitive information such API keys and passwords is involved it presents a security issue

ConfigMaps and secrets

- Separate configuration from Pod specs
- Results in easier to manage and more portable manifests
- Both are similar but secrets are specifically for sensitive data
- There are specialized types of Secrets for storing Docker registry credential and TLS certs

Using configMaps and secrets

- Data store in key value pairs
- Pods must reference ConfigMaps and secrets to use their data
- References can be made by mounting Volumes or setting environment variables that

Example: ConfigMap

10.2-data_tier_config.yaml

Example: Secrets

10.4-app_tier_secret.yaml














