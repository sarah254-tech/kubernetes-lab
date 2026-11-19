# Kubernetes Hands-on Labs

A practical collection of Kubernetes exercises completed as part of the **DMI DevOps Micro Internship**.

This repository brings together hands-on Kubernetes labs from Assignments 1–9, covering the deployment, management, networking, health monitoring, and scaling of containerised applications.

Throughout these exercises, **NGINX** was used as the sample application to explore Kubernetes resources and understand how Kubernetes manages application workloads in a cluster.

## Repository Overview

The labs are organised by Kubernetes concept, with YAML manifests for creating resources, testing configurations, introducing failures, and observing Kubernetes behaviour.

```text
k8s-labs/
│
├── autoscaling/
│   ├── autohealing-deployment.yaml
│   ├── hpa-deployment.yaml
│   └── hpa-nginx.yaml
│
├── deployments/
│   └── nginx-deployment.yaml
│
├── health-probes-liveness/
│   ├── 00-nginx-deploy-baseline.yaml
│   ├── 01-nginx-deploy-liveness.yaml
│   └── 02-nginx-liveness-broken.yaml
│
├── health-probes-readiness/
│   ├── 00-nginx-deploy-baseline.yaml
│   ├── 01-nginx-deploy-readiness.yaml
│   ├── 02-nginx-readiness-broken.yaml
│   └── 04-readiness-broken-patch.yaml
│
├── pods/
│   └── nginx-pod.yaml
│
├── replicasets/
│   └── nginx-replicaset.yaml
│
└── services/
    ├── clusterip/
    ├── loadbalancer/
    └── nodeport/
```

## Labs Covered

### 1. Pods

Introduction to Kubernetes Pods, the smallest deployable units in Kubernetes.

**What I explored:**
- Creating an NGINX Pod using a Kubernetes YAML manifest.
- Understanding how Pods run containers.
- Inspecting Pod status and verifying application availability.

### 2. Deployments

Exploring how Kubernetes Deployments manage application workloads.

**What I explored:**
- Creating an NGINX Deployment.
- Managing replicas.
- Performing rolling updates.
- Updating the NGINX image from `1.21.1` to `1.23.1`.
- Rolling back to a previous application version.
- Scaling replicas from 2 to 5 and back to 2.
- Understanding rolling update strategies using `maxSurge` and `maxUnavailable`.

### 3. ReplicaSets

Understanding how ReplicaSets maintain the desired number of running Pods.

**What I explored:**
- Creating an NGINX ReplicaSet.
- Defining the desired replica count.
- Understanding how Kubernetes maintains the desired number of Pods.

### 4. Autoscaling and Self-Healing

Exploring Kubernetes workload resilience and automatic scaling.

**What I explored:**
- Deploying an NGINX application with an auto-healing Deployment.
- Deleting a Pod and observing Kubernetes automatically create a replacement.
- Configuring a Horizontal Pod Autoscaler (HPA).
- Defining CPU resource requests and limits.
- Configuring minimum and maximum replica counts.
- Setting a target CPU utilisation of 50%.

The HPA exercise used a minimum of 2 replicas and a maximum of 5, with a CPU request of `100m` and limit of `200m`.

### 5. Liveness Probes

Understanding how Kubernetes checks whether a container is healthy and should continue running.

**What I explored:**
- Configuring HTTP liveness probes for NGINX.
- Using port 80 for health checks.
- Introducing an invalid health-check path.
- Observing failed health checks and container restarts.
- Understanding how repeated failures can result in `CrashLoopBackOff`.

### 6. Readiness Probes

Understanding how Kubernetes determines whether an application is ready to receive traffic.

**What I explored:**
- Configuring HTTP readiness probes.
- Testing application readiness on port 80.
- Introducing an invalid readiness endpoint.
- Observing how an unready Pod is excluded from Service endpoints.
- Correcting broken readiness configurations.
- Understanding the relationship between readiness probes and application availability.

### 7. Kubernetes Services

Exploring how Kubernetes exposes applications and enables communication between workloads.

The Service labs cover three Service types:

**ClusterIP**
- Creating an internal Kubernetes Service.
- Exposing NGINX within the cluster.
- Understanding Service discovery through DNS.
- Testing communication using the Service name and fully qualified domain name (FQDN).
- Investigating broken selectors and empty endpoints.

**NodePort**
- Exposing an NGINX application through a port on a Kubernetes node.
- Testing access through the node IP and NodePort.
- Using a test Pod to investigate application connectivity.
- Breaking and restoring Service selectors.
- Observing how Service endpoints change when Pods are replaced.

**LoadBalancer**
- Defining a Kubernetes LoadBalancer Service for the NGINX application.
- Exploring the configuration used to expose an application through an external load-balancing service.

## Key Kubernetes Concepts Practised

| Area | Concepts |
|---|---|
| Workloads | Pods, Deployments, ReplicaSets |
| Application management | Scaling, rolling updates, rollbacks |
| Resilience | Self-healing and Pod replacement |
| Health monitoring | Liveness and readiness probes |
| Networking | ClusterIP, NodePort, LoadBalancer |
| Service discovery | Labels, selectors, DNS and endpoints |
| Autoscaling | Horizontal Pod Autoscaler and CPU utilisation |

## Working with the Lab Manifests

The repository contains YAML configuration files that can be applied to a Kubernetes cluster using `kubectl`.

For example:

```bash
# Create a Kubernetes Deployment
kubectl apply -f deployments/nginx-deployment.yaml

# View running Pods
kubectl get pods

# View Deployments
kubectl get deployments

# View Services
kubectl get services

# View ReplicaSets
kubectl get replicasets

# Inspect a specific resource
kubectl describe deployment nginx-deployment
```

To remove a resource created from a manifest:

```bash
kubectl delete -f deployments/nginx-deployment.yaml
```

**Note:** Some manifests intentionally contain broken configurations for troubleshooting exercises. Review the YAML before applying it, particularly the files labelled `broken`.

## Learning Outcomes

Through these practical exercises, I developed hands-on experience with:

- Writing and managing Kubernetes YAML manifests.
- Deploying and managing containerised applications.
- Understanding the relationship between Pods, ReplicaSets and Deployments.
- Managing application updates, rollbacks and scaling.
- Implementing application health checks.
- Troubleshooting readiness and liveness failures.
- Understanding Kubernetes networking and Service discovery.
- Exploring application resilience through self-healing and autoscaling.

## About This Repository

This repository serves as a practical record of my Kubernetes learning journey during the DMI DevOps Micro Internship.

Rather than simply learning Kubernetes commands, these exercises provided an opportunity to configure resources, observe application behaviour, deliberately introduce failures, troubleshoot problems and understand how Kubernetes maintains application availability.

**Technology:** Kubernetes, NGINX, YAML, kubectl

**Repository:** [kubernetes-lab](https://github.com/sarah254-tech/kubernetes-lab)
