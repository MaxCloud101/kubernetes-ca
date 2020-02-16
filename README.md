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

To see a log from specific container in pod

```
kubectl logs -n microservice app counter
```

To see logs in real time in specific container

```
kubectl logs -n microservice app poller -f
```




















