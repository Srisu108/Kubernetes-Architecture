# Kubernetes-Architecture
Basic K8's Architecture

🧩 Kubernetes Architecture – Control Plane & Data Plane

A simple, clear explanation based on my learning journey.

📌 Overview

Kubernetes (K8s) is a container orchestration system that automates deployment, scaling, and management of containerized applications.
Its architecture is built around two main components:

Control Plane – The brain of Kubernetes

Data Plane (Worker Nodes) – Where application Pods actually run

This document breaks down each component in a clean, beginner-friendly way.

🧠 Control Plane Architecture

The Control Plane manages the overall cluster state and decision-making.

          +-----------------------------+
          |        CONTROL PLANE        |
          |-----------------------------|
          |  API Server                 |
          |  Scheduler                  |
          |  etcd                       |
          |  Controller Manager         |
          |  Cloud Controller Manager   |
          +-----------------------------+

🔗 API Server

Acts as the central communication hub for Kubernetes.

All interactions (kubectl, controllers, kubelets) pass through it.

Considered the heart of the cluster.

🧮 Scheduler

Assigns Pods to worker nodes.

Makes placement decisions based on:

Node resources

Constraints

Affinity rules

Workload distribution

🗄️ etcd

A distributed key-value store.

Stores the entire cluster state, including:

Pod specs

Configurations

Secrets

Node information

Critical for backup & disaster recovery.

🔄 Controller Manager

Ensures the desired state = actual state.

Examples of controllers:

ReplicaSet Controller

Deployment Controller

Node Controller

If something drifts from the desired state, controllers bring it back to normal.

☁️ Cloud Controller Manager (CCM)

Responsible for interacting with the cloud provider.

Handles:

Load balancers

Volume provisioning

Node lifecycle

Routing

⚙️ Data Plane (Worker Nodes)

Worker nodes run workloads (Pods/containers) and report to the Control Plane.

        +-----------------------------+
        |          DATA PLANE         |
        |-----------------------------|
        |  Kubelet                    |
        |  Kube-proxy                 |
        |  Container Runtime          |
        +-----------------------------+

🛠️ 1. Container Runtime

Responsible for starting and running containers.

Supported runtimes:

Containerd

CRI-O

Docker (legacy, via Dockershim – now deprecated)

🔍 2. Kubelet

Runs on every worker node.

Responsible for:

Ensuring Pods are running

Reporting node/pod status

Acting on instructions from the API Server

Supports self-healing by restarting failed Pods.

🌐 3. Kube-proxy

Manages networking on each node.

Performs service routing using:

iptables

IPVS

Ensures traffic reaches the correct Pod.

🆚 Docker vs Kubernetes Networking & Runtime
Topic	Docker	Kubernetes
Networking	Docker Bridge Network	Kube-proxy using IP tables/IPVS
Runtime	Docker Engine	CRI runtimes (Containerd / CRI-O)

Historically, Kubernetes used Docker via Dockershim, but modern clusters rely on CRI runtimes.

🧩 Summary

Kubernetes cleanly separates responsibilities:

Control Plane → Makes decisions

Data Plane → Executes decisions and runs workloads

Understanding this architecture builds a strong foundation for mastering deployments, autoscaling, networking, and cluster operations.
