# Certified Kubernetes Administrator (CKA) Exam Requirements: A Comprehensive Guide

Welcome to my CKA practice YAML and Markdown repository! This README serves as a comprehensive guide to the Certified Kubernetes Administrator (CKA) exam, outlining the key requirements across various domains. The CKA exam is a hands-on, performance-based test that validates your ability to administer and manage Kubernetes clusters in a real-world environment. To pass, you'll need to achieve a score of **66% or higher** within the **2-hour** exam duration.

This repository is designed to complement your CKA preparation, with a dedicated `yaml-files` folder containing practical Kubernetes configurations and an `md-files` folder for detailed explanations and study notes.

Let's dive into the core domains and their essential requirements:

---

## 1. Cluster Architecture, Installation & Configuration (25%)

This domain focuses on your ability to set up, maintain, and upgrade Kubernetes clusters.

* **Kubernetes Fundamentals:**
    * Understand Kubernetes architecture: Control Plane (kube-apiserver, etcd, kube-scheduler, kube-controller-manager, cloud-controller-manager) and Worker Nodes (kubelet, kube-proxy, container runtime).
    * Familiarity with `kubectl` for interacting with the cluster.
    * Understanding of API objects and their definitions (e.g., Pods, Deployments, Services).

* **Cluster Installation with Kubeadm:**
    * **Prerequisites:** Setting up nodes with necessary packages (container runtime, `kubeadm`, `kubelet`, `kubectl`).
    * **Initializing the Control Plane:** Using `kubeadm init` to bootstrap the control plane.
    * **Joining Worker Nodes:** Using `kubeadm join` to add worker nodes to the cluster.
    * **Configuring a Pod Network Add-on:** Deploying a CNI plugin (e.g., Calico, Flannel) to enable pod-to-pod communication.

* **Cluster Administration & Maintenance:**
    * **etcd Backup and Restore:** Performing backups of the etcd database and restoring the cluster from a backup.
    * **Kubeadm Cluster Upgrades:** Upgrading a Kubernetes cluster to a new version using `kubeadm`.
    * **Managing High Availability (HA) Clusters:** Understanding stacked etcd topology and external etcd configurations for HA.
    * **Node Maintenance:** Draining and cordoning nodes for maintenance, then uncordoning them.
    * **Managing RBAC (Role-Based Access Control):** Creating and managing Roles, ClusterRoles, RoleBindings, and ClusterRoleBindings to control access to cluster resources.
    * **kubeconfig:** Managing `kubeconfig` files and contexts for different clusters and users.

---

## 2. Workloads & Scheduling (15%)

This section tests your knowledge of deploying and managing applications, and how Kubernetes schedules them across nodes.

* **Pod Management:**
    * Creating and managing Pods, including multi-container Pods.
    * Understanding Pod lifecycle (Pending, Running, Succeeded, Failed, Unknown).
    * **Init Containers:** Using Init Containers for setup tasks before the main application containers start.
    * **Probes (Liveness and Readiness):** Implementing health checks for application containers.
    * **Resource Requests and Limits:** Defining CPU and memory requests and limits for containers.
    * **ConfigMaps and Secrets:** Using ConfigMaps for non-sensitive configuration data and Secrets for sensitive information, and mounting them as volumes or environment variables.

* **Controllers:**
    * **Deployments:** Creating, managing, performing rolling updates and rollbacks, and scaling Deployments.
    * **ReplicaSets:** Understanding and managing ReplicaSets, often implicitly created by Deployments.
    * **DaemonSets:** Deploying DaemonSets to ensure a Pod runs on all (or a subset of) nodes.
    * **StatefulSets:** Understanding StatefulSets for stateful applications, including stable network identities and persistent storage.

* **Scheduling:**
    * **Node Affinity/Anti-affinity:** Controlling which nodes Pods are scheduled on or avoided.
    * **Taints and Tolerations:** Preventing Pods from being scheduled on specific nodes (taints) and allowing Pods to be scheduled on tainted nodes (tolerations).
    * **Resource Quotas and LimitRanges:** Enforcing resource consumption limits at the namespace level.
    * **Horizontal Pod Autoscaler (HPA):** Configuring HPA to automatically scale the number of Pod replicas based on metrics.

---

## 3. Services & Networking (20%)

This domain covers how applications communicate within and outside the cluster.

* **Kubernetes Networking Fundamentals:**
    * Understanding the basic networking model (Pod IP, Cluster IP, NodePort, LoadBalancer, Ingress).
    * Connectivity between Pods.
    * How `kube-proxy` enables Service communication.

* **Service Types:**
    * **ClusterIP:** Exposing a Service within the cluster.
    * **NodePort:** Exposing a Service on a static port on each node's IP.
    * **LoadBalancer:** Exposing a Service externally using a cloud provider's load balancer.
    * **ExternalName:** Mapping a Service to an external DNS name.

* **Ingress:**
    * Understanding Ingress resources for external access to services, including routing rules.
    * Familiarity with Ingress Controllers (though you won't typically install one from scratch in the exam, understanding their role is key).

* **Network Policies:**
    * Defining and enforcing Network Policies to control network traffic between Pods and namespaces.

* **CoreDNS:**
    * Understanding how CoreDNS provides service discovery within the cluster.
    * Troubleshooting DNS resolution issues for Pods and Services.

---

## 4. Storage (10%)

This section focuses on managing persistent storage for applications in Kubernetes.

* **Persistent Volumes (PVs):**
    * Understanding PVs as abstract pieces of storage in the cluster.
    * Configuring various volume types (e.g., hostPath, NFS, cloud provider specific).
    * Understanding access modes (ReadWriteOnce, ReadOnlyMany, ReadWriteMany) and reclaim policies (Retain, Recycle, Delete).

* **Persistent Volume Claims (PVCs):**
    * Creating and managing PVCs to request storage from PVs.
    * Binding PVCs to Pods.

* **StorageClasses:**
    * Understanding StorageClasses for dynamic provisioning of Persistent Volumes.
    * Defining StorageClasses with different provisioners and parameters.

* **Volume Snapshots:**
    * Understanding the concept of volume snapshots (though direct creation might not be a primary exam task, it's good to be aware).

---

## 5. Troubleshooting (30%)

This is the largest and arguably most critical domain, evaluating your ability to diagnose and resolve issues within a Kubernetes cluster.

* **Troubleshooting Clusters and Nodes:**
    * **Cluster Component Failure:** Diagnosing issues with control plane components (kube-apiserver, etcd, scheduler, controller-manager) and worker node components (kubelet, kube-proxy).
    * **Node Status:** Checking node status (`kubectl get nodes`), descriptions (`kubectl describe node`), and logs.
    * **Resource Exhaustion:** Identifying issues related to CPU, memory, or disk exhaustion on nodes.

* **Troubleshooting Application Failure:**
    * **Pod Status:** Checking Pod status (`kubectl get pods`), descriptions (`kubectl describe pod`), and events.
    * **Container Logs:** Accessing container logs (`kubectl logs`) and understanding standard output/error streams.
    * **Application-level Issues:** Diagnosing application failures within containers (e.g., misconfigurations, dependencies, errors).
    * **Deployment Rollout Status:** Monitoring rollout status and performing rollbacks.

* **Troubleshooting Services and Networking:**
    * **Service Endpoints:** Verifying Service endpoints and their association with Pods.
    * **Network Connectivity:** Diagnosing network issues between Pods, between Pods and Services, and external access problems.
    * **DNS Resolution:** Troubleshooting DNS issues for service discovery.
    * **Network Policies:** Ensuring Network Policies are not inadvertently blocking traffic.
    * **`kube-proxy` issues:** Diagnosing issues with `kube-proxy`'s role in service networking.

* **General Troubleshooting Techniques:**
    * Using `kubectl describe` for detailed information on resources.
    * Using `kubectl events` to see cluster events.
    * Leveraging `journalctl` or direct log files for system-level component logs.
    * Using `crictl` for inspecting container runtime issues (if applicable).
    * Understanding common `sysctl` parameters related to networking (e.g., `net.ipv4.ip_forward`).

---

## How to Use This Repository

The `yaml-files` folder contains practical examples of Kubernetes resources that you can use to practice creating, modifying, and troubleshooting. The `md-files` folder will house more detailed explanations and notes for each of the CKA domains.

**Getting Started:**

1.  **Clone this repository:** `git clone <repo-url>`
2.  **Navigate to `yaml-files`:** Explore the YAML files for various Kubernetes objects.
3.  **Practice:** Spin up a local Kubernetes cluster (e.g., minikube, kind) and apply these YAMLs. Experiment with different configurations and observe the outcomes.
4.  **Refer to `md-files`:** Use the Markdown files for in-depth explanations of concepts and best practices for each domain.
5.  **Troubleshoot:** Intentionally introduce errors into your YAMLs or cluster to practice your troubleshooting skills.

