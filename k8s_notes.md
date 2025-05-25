# Kubernetes Notes 

## What is Kubernetes?

Kubernetes (K8s) is a container orchestration system that automates the deployment, scaling, and management of containerized applications across multiple servers.

## Why "K8s"?

"Kubernetes" becomes "K8s" because there are 8 letters between 'K' and 's'.

##  What does Kubernetes do?

Kubernetes handles:
1. Automatic Deployment
2. Load Balancing
3. Auto-scaling
4. Monitoring & Self-healing
5. Supports various container runtimes (Docker, CRI-O, containerd)

## What is a Pod?

A Pod is the smallest unit in Kubernetes. It can contain one or more containers that share the same storage and network.

##  Kubernetes Cluster Structure

A Kubernetes Cluster has:
* 1 Master Node: Controls the cluster (control plane)
* Many Worker Nodes: Run your actual applications (Pods)

## Key Services on Nodes

Each Node runs:
* `kubelet` (talks to Master)
* `kube-proxy` (network routing)
* Container Runtime (e.g. Docker)

##  Tools You Need

You need 3 tools:
1. `kubectl`: Command-line tool to control Kubernetes
2. `minikube`: Create a local Kubernetes cluster
3. VS Code: For editing YAML & code

## Minikube Notes

Minikube creates a single-node cluster for learning. It needs a virtual machine manager like VirtualBox (macOS) or Hyper-V (Windows).

### 1. What is the primary role of the Master Node in a Kubernetes cluster?

To manage the cluster's resources and orchestrate the deployment of applications

### 2. Which of the following are key services running on the Master Node in a Kubernetes cluster?

* etcd
* DNS service
* API Server
* kube-controller-manager

### 3. Which of the following concepts are part of Kubernetes' auto-scaling capabilities?

* Vertical Pod Autoscaler
* Cluster Autoscaler
* Horizontal Pod Autoscaler

### 4. What is the primary purpose of Minikube in a Kubernetes setup?

To create a local Kubernetes cluster on a single node

### 5. Which of the following are steps to install Minikube on a Windows operating system?

* Install Hyper-V or VirtualBox
* Download Minikube executable

1. What is minikube start used for?

Start a local single-node Kubernetes cluster using a specified VM driver.

2. What is the default container runtime used by Minikube?

Minikube uses Docker as the default container runtime.

3. How to access the Minikube node and list containers inside?

Use SSH to connect and docker ps to list containers running inside the Minikube node.

4. How to create a Pod using kubectl?

Use kubectl run with an image to create a single Pod.

5. What is the pause container in each Pod?

The pause container keeps the Pod's network namespace stable.

6. How to check Pod details and IP address?

Use kubectl describe pod <name> to see full details including IP and node info.

7. Can you access Pod via its internal IP from your host?

No, Pod IPs are internal and not accessible from outside.

8. How to delete a Pod?

Use kubectl delete pod <name> to remove a Pod.

9. How to shorten kubectl with an alias?

Create a terminal alias like alias k="kubectl" for convenience.

## 1. What is Deployment scaling in Kubernetes?

You can scale a deployment to run multiple Pods using the `kubectl scale` command.

## 2. Can we reduce the number of Pods in a Deployment?

Yes, you can scale down to reduce the number of running Pods.

## 3. How does Kubernetes name Pods in a Deployment?

Pods are named with the ReplicaSet prefix followed by a unique suffix.

## 4. Do all Pods get unique IPs?

Yes, each Pod gets its own internal IP address within the cluster.

## 5. Can you access Pod IPs from outside the cluster?
No, Pod IPs are internal and cannot be accessed from your computer.

## 6. How to access Pods from within the cluster?

SSH into the node and use `curl <Pod IP>` to test the web server.

## 7. Why not rely on Pod IPs for service connection?

Pod IPs change when Pods are recreated, so it’s unreliable to hardcode them.

You scale a Deployment to run multiple Pods, but to access them reliably, use a Service instead of Pod IPs.

## 1. What is a Kubernetes Service?

A Service in Kubernetes provides a stable network endpoint to access a group of Pods.

## 2. What is a ClusterIP Service?

ClusterIP exposes the deployment internally within the cluster and cannot be accessed from outside.

## 3. How to view created Services?

Use `kubectl get svc` or `kubectl get services` to list all services.

## 4. Why can’t you access ClusterIP from your computer?

Because ClusterIP only works inside the Kubernetes cluster.

## 5. How to test a ClusterIP Service?

SSH into the Minikube node and use `curl` with the ClusterIP and port.

## 6. How does Kubernetes know which Pods to route traffic to?

It uses `label selectors` to match Pods and Services.

## 7. How to delete a Deployment and Service?

Use `kubectl delete` to clean up old resources.

ClusterIP Service allows access to a Deployment inside the cluster via a stable virtual IP, making internal communication reliable and load-balanced.

## 1. What is a Node.js Dockerized App in Kubernetes?

A custom Node.js app can be packaged into a Docker image, pushed to Docker Hub, and deployed in Kubernetes.

## 2. What is `kubectl create deployment` with a custom image?

Use `kubectl create deployment` to deploy your custom image from Docker Hub.

## 3. What is a ClusterIP / NodePort / LoadBalancer service?

### A. ClusterIP

Default internal IP, used only inside the cluster.

### B. NodePort

Exposes the app on a port of the Node (host), accessible from your computer.

### C. LoadBalancer

Used in cloud setups, provides an external IP (pending in Minikube).

## 4. What is Load Balancing in Kubernetes?

Kubernetes automatically distributes traffic to different Pods behind a Service.

## 5. How to scale a deployment?

Use `kubectl scale` to increase or decrease the number of Pods.

## 6. How to check deployment logs & configuration?

Use `kubectl describe` to view deployment/service details.

You can build and deploy a custom Node.js app on Kubernetes, expose it via ClusterIP, NodePort or LoadBalancer, and scale it easily with a single command.

#### 1. What is RollingUpdate?
> RollingUpdate is a deployment strategy in Kubernetes that updates Pods gradually without downtime.

#### 2. How to update a deployment?
> Use `kubectl set image` to point the deployment to a new image version, and `kubectl rollout status` to track the update.

#### 3. What happens if a Pod is deleted manually?
> Kubernetes automatically recreates the deleted Pod to maintain the desired number of replicas.

#### 4. How to launch the Kubernetes Dashboard?
> Use `minikube dashboard` to open a GUI to monitor deployments, Pods, ReplicaSets, and services.

#### 5. What is declarative approach in Kubernetes?
> Instead of using CLI commands to create resources, write YAML files and apply them with `kubectl apply -f`.

```bash
kubectl rollout status deployment/k8s-web-hello
```

```bash
minikube dashboard
```

```bash
kubectl rollout status deployment/k8s-web-hello
```

```bash
kubectl get pods
kubectl delete pod [pod-name]
kubectl get pods
```

```bash
kubectl apply -f deployment.yaml
```

```bash
kubectl apply -f service.yaml
```

```bash
minikube service k8s-web-hello
```

### 1. What is a Deployment?
> A Deployment manages a ReplicaSet which in turn manages Pods.

### 2. What is a Service?
> A Service provides a stable network endpoint to access Pods.

### 3. What is a ClusterIP Service?
> A ClusterIP service is only accessible from inside the cluster.

### 4. What is a NodePort Service?
> A NodePort service exposes Pods on a static port of each Node.

### 5. What is a LoadBalancer Service?
> A LoadBalancer service provisions an external IP (on cloud) to access Pods.

### 6. What is RollingUpdate?
> RollingUpdate gradually replaces old Pods with new ones during an update.

### 7. What is a Declarative Approach?
> Declarative means describing the desired state in YAML, and letting Kubernetes make it happen.

### 8. How do Deployments Communicate?
> Services allow one Deployment to talk to another using service names.

### 9. What is CRI-O?
> CRI-O is a lightweight container runtime compatible with Kubernetes.

```bash
kubectl get pods -o wide
```

```bash
kubectl create deployment nginx-deployment --image=nginx
```

```bash
kubectl scale deployment nginx-deployment --replicas=5
```

```bash
kubectl expose deployment nginx-deployment --port=8080 --target-port=80
```

```bash
kubectl expose deployment nginx-deployment --type=NodePort --port=3000
```

```bash
kubectl set image deployment/nginx-deployment nginx=nginx:1.19
```

```bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

```bash
kubectl exec -it pod-name -- nslookup nginx
```
