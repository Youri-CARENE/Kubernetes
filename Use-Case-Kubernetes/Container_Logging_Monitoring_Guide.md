
# Container Logging and Monitoring Guide

## Logging

### Docker Logging
#### Run a Container and Check Logs
```bash
docker run kodekloud/event-simulator
```
To run in detached mode and check logs:
```bash
docker run -d kodekloud/event-simulator
docker logs -f <container_id>
```

#### Example Logs
```
2018-10-06 15:57:15,937 - root - INFO - USER1 logged in
2018-10-06 15:57:16,943 - root - INFO - USER2 logged out
2018-10-06 15:57:17,944 - root - INFO - USER2 is viewing page2
2018-10-06 15:57:18,951 - root - INFO - USER3 is viewing page3
2018-10-06 15:57:19,954 - root - INFO - USER4 is viewing page1
...
```

### Kubernetes Logging
#### Create a Pod and Check Logs
1. Define the Pod in a YAML file (`event-simulator.yaml`):
    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
      name: event-simulator-pod
    spec:
      containers:
      - name: event-simulator
        image: kodekloud/event-simulator
    ```
2. Create the Pod:
    ```bash
    kubectl create -f event-simulator.yaml
    ```
3. View Logs:
    ```bash
    kubectl logs -f event-simulator-pod
    ```

#### Example Logs
```
2018-10-06 15:57:15,937 - root - INFO - USER1 logged in
2018-10-06 15:57:16,943 - root - INFO - USER2 logged out
2018-10-06 15:57:17,944 - root - INFO - USER2 is viewing page2
2018-10-06 15:57:18,951 - root - INFO - USER3 is viewing page3
2018-10-06 15:57:19,954 - root - INFO - USER4 is viewing page1
...
```

---

## Monitoring

### Metrics Server
#### Installing Metrics Server
1. Enable metrics-server in Minikube:
    ```bash
    minikube addons enable metrics-server
    ```
2. Clone the repository and deploy:
    ```bash
    git clone https://github.com/kubernetes-incubator/metrics-server.git
    kubectl create -f deploy/1.8+/
    ```

#### Commands to View Metrics
- **View Node Metrics**:
    ```bash
    kubectl top node
    ```
    Example Output:
    ```
    NAME          CPU(cores)   CPU%   MEMORY(bytes)   MEMORY%
    kubemaster    166m         8%     1337Mi          70%
    kubenode1     36m          1%     1046Mi          55%
    kubenode2     39m          1%     1048Mi          55%
    ```

- **View Pod Metrics**:
    ```bash
    kubectl top pod
    ```
    Example Output:
    ```
    NAME      CPU(cores)   CPU%   MEMORY(bytes)   MEMORY%
    nginx     166m         8%     1337Mi          70%
    redis     36m          1%     1046Mi          55%
    ```

#### Notes
- Metrics-server replaced Heapster in recent Kubernetes versions.
- `play-with-k8s` (version 1.8) still requires Heapster.

---

## References
- [Core Metrics Pipeline](https://kubernetes.io/docs/tasks/debug-application-cluster/core-metrics-pipeline/)
- [Resource Usage Monitoring](https://kubernetes.io/docs/tasks/debug-application-cluster/resource-usage-monitoring/)
- [Manage Resources](https://kubernetes.io/docs/tasks/administer-cluster/manage-resources/)
