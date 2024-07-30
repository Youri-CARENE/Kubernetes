
# Kubernetes Basic Architecture

---

## 1. Introduction to Kubernetes

Kubernetes is an open-source container management platform that automates the deployment, scaling, and operations of containerized applications.

---

## 2. Kubernetes Architecture

The architecture of Kubernetes is composed of several components distributed between the **Control Plane** and the **Worker Nodes**.

---

### A. Control Plane

The Control Plane manages the entire Kubernetes cluster. It is responsible for making global decisions about the cluster and detecting and responding to cluster events.

1. **API Server (kube-apiserver)**
   - **Role**: Exposes the Kubernetes API.
   - **Function**: Central communication point for all Kubernetes components and the main interface for cluster administration.

2. **Etcd**
   - **Role**: Configuration data storage.
   - **Function**: Distributed key-value database that stores all cluster state information.

3. **Scheduler (kube-scheduler)**
   - **Role**: Pod scheduling to nodes.
   - **Function**: Schedules unassigned pods to nodes based on available resources and defined constraints.

4. **Controller Manager (kube-controller-manager)**
   - **Role**: Execution of controllers.
   - **Function**: Manages various controllers like ReplicaSet, Deployment, DaemonSet, ensuring the cluster's actual state matches the desired state.

---

### B. Worker Nodes

Worker Nodes run the containerized applications. Each node has the necessary services to run pods and is managed by the Control Plane.

1. **Kubelet**
   - **Role**: Node agent.
   - **Function**: Ensures containers are running in pods, interacts with the control plane to get necessary information, and controls pod state.

2. **Kube-proxy**
   - **Role**: Cluster network management.
   - **Function**: Maintains network rules on nodes, enabling pod network communication and load balancing network traffic.

3. **Container Runtime**
   - **Role**: Container execution.
   - **Function**: Runs and manages the lifecycle of containers (such as Docker, containerd).

---

### C. Kubernetes Architecture Diagram

```plaintext
+------------------------------------+
|            Control Plane           |
+------------------------------------+
|                                    |
|  +-----------------------------+   |
|  |        kube-apiserver       |   |
|  +-----------------------------+   |
|  |            etcd             |   |
|  +-----------------------------+   |
|  |      kube-scheduler         |   |
|  +-----------------------------+   |
|  |  kube-controller-manager    |   |
|  +-----------------------------+   |
|                                    |
+------------------------------------+
                |
                |
                v
+------------------------------------+
|           Worker Nodes             |
+------------------------------------+
|                                    |
|  +-----------------------------+   |
|  |           Kubelet           |   |
|  +-----------------------------+   |
|  |          Kube-proxy         |   |
|  +-----------------------------+   |
|  |     Container Runtime       |   |
|  +-----------------------------+   |
|                                    |
|  +-----------------------------+   |
|  |           PODS              |   |
|  |  +----------------------+   |   |
|  |  |  Containers          |   |   |
|  |  +----------------------+   |   |
|  +-----------------------------+   |
|                                    |
+------------------------------------+
```

---

## 3. General Workflow

- **Application Deployment**: Users define applications in YAML configuration files. These files are sent to the API Server.
- **Scheduling and Allocation**: The Scheduler assigns pods to available nodes.
- **Execution**: The Kubelet on each node runs the containers defined in the pods.
- **Networking and Services**: Kube-proxy manages network communication between pods and the outside world.

---

### Conclusion

Kubernetes provides flexible and powerful container orchestration, ensuring high availability, automatic scaling, and simplified management of containerized applications.
