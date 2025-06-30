# centos-k8s
A Vagrant-based Kubernetes v1.33 cluster setup using CentOS 9 and kubeadm. The cluster consists of 1 master node and 2 worker nodes.

# Kubernetes v1.33 Cluster with Vagrant and CentOS 9

This repository provides a Vagrant-based setup to create a local Kubernetes cluster (v1.33) using CentOS Stream 9 and `kubeadm`.

## 📦 Cluster Topology

- 1 Master Node
- 2 Worker Nodes
- All nodes are provisioned using Vagrant and VirtualBox
- Kubernetes is installed using `kubeadm`

## 🧰 Tools & Versions

- Kubernetes: v1.33
- OS: CentOS Stream 9
- Vagrant: >= 2.x
- VirtualBox: >= 6.x

## 🚀 Getting Started

1. Clone this repository
   ```bash
   git clone https://github.com/your-username/k8s-vagrant-cluster-centos9-kubeadm.git
   cd k8s-vagrant-cluster-centos9-kubeadm
