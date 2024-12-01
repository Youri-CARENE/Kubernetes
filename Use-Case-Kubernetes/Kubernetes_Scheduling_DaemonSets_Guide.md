
# Kubernetes Scheduling and Daemon Sets Guide

## Course Objectives
- **Scheduling**
- **Application Lifecycle Management**
- **Cluster Maintenance**
- **Logging Monitoring**
- **Security**
- **Storage**
- **Troubleshooting**
- **Labels & Selectors**
- **Daemon Sets**
- **Resource Limits**
- **Multiple Schedulers**
- **Manual Scheduling**
- **Scheduler Events**
- **Configure Kubernetes Scheduler**

---

## Manual Scheduling

### How Scheduling Works

#### Example Pod Definition
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
  labels:
    name: nginx
spec:
  containers:
  - name: nginx
    image: nginx
    ports:
    - containerPort: 8080
  nodeName: node01
```

#### Steps to Schedule:
1. **Define the `nodeName`** field in the pod specification to manually bind the pod to a node.
2. **Verify Pod Status** using:
   ```bash
   kubectl get pods
   ```
3. **Example Output**:
   - Before scheduling: `Pending`
   - After scheduling: `Running`

#### Example Binding with API
```yaml
apiVersion: v1
kind: Binding
metadata:
  name: nginx
target:
  apiVersion: v1
  kind: Node
  name: node02
```
Use `curl` to manually bind the pod to a node.

---

## Daemon Sets

### Use Cases
- Deploy monitoring agents on each node.
- Distribute network components such as `kube-proxy` or `weave-net`.

### Example DaemonSet Definition
```yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: monitoring-daemon
spec:
  selector:
    matchLabels:
      app: monitoring-agent
  template:
    metadata:
      labels:
        app: monitoring-agent
    spec:
      containers:
      - name: monitoring-agent
        image: monitoring-agent
```

### Commands
- **Create DaemonSet**:
  ```bash
  kubectl create -f daemon-set-definition.yaml
  ```
- **View DaemonSets**:
  ```bash
  kubectl get daemonsets
  ```
- **Describe DaemonSet**:
  ```bash
  kubectl describe daemonsets monitoring-daemon
  ```

---

## Multiple Schedulers

### Deploying a Custom Scheduler

#### Steps to Deploy:
1. Download the `kube-scheduler` binary.
   ```bash
   wget https://storage.googleapis.com/kubernetes-release/release/v1.12.0/bin/linux/amd64/kube-scheduler
   ```
2. Create a new service for the custom scheduler.
   ```yaml
   ExecStart=/usr/local/bin/kube-scheduler \
   --config=/etc/kubernetes/config/kube-scheduler.yaml \
   --scheduler-name=my-custom-scheduler
   ```

#### Example Scheduler Pod Definition
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-custom-scheduler
  namespace: kube-system
spec:
  containers:
  - command:
    - kube-scheduler
    - --address=127.0.0.1
    - --kubeconfig=/etc/kubernetes/scheduler.conf
    - --leader-elect=true
    - --scheduler-name=my-custom-scheduler
    image: k8s.gcr.io/kube-scheduler-amd64:v1.11.3
```

#### Verify Schedulers
```bash
kubectl get pods --namespace=kube-system
```

---

## Security Best Practices

### Objectives
- **Authentication & Authorization**
- **Network Policies**
- **TLS Certificates**
- **Secure Image Management**
- **Security Contexts**

### Example Security Context in Pod
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: secure-pod
spec:
  containers:
  - name: nginx
    image: nginx
    securityContext:
      runAsUser: 1000
      runAsGroup: 3000
      readOnlyRootFilesystem: true
```

---

This document provides a comprehensive overview of Kubernetes scheduling, daemon sets, and security configurations.
