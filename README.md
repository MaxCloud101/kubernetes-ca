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










