# Command-Line Review Sheet
## MiniKube
* **Start** the MiniKube cluster
    ```bash
    minikube start
    ```
* **Stop** the MiniKube cluster
    ```bash
    minikube stop
    ```
* Check the **Status** of MiniKube cluster
    ```bash
    minikube status
    ```

## `kubectl` 
* Check cluster info
    ```bash
    kubectl cluster-info
    ```
* List nodes of the cluster
    ```bash
    kubectl get nodes
    ```
## PODs
* Run a _Pod_ based on an image
    * Name: nginx-app
    * Image: nginx
    ```bash
    kubectl run nginx-app --image nginx
    ```
    * An alternative is to use option `-o yaml` to run a _Pod_ then **output** the YAML file
       ```bash
       kubectl run nginx-app --image nginx -o yaml > nginx.yml 
       ```

* List Pods on the cluster
    ```bash
    kubectl get pods
    ```
* List Pods on the cluster with more info
   ```bash
   kubectl get pods -o wide
   ```
* Get more detailed info about a _Pod_
    ```bash
    kubectl describe pod nginx
    ```
* POD definition file example
    ```yml
    apiVersion: v1
    kind: Pod
    metadata:
    name: myapp-pod
    labels:
        app: myapp 
    spec:
    containers:
    - name: nginx-container
        image: nginx
    ```
* Create a _Pod_ based on _YAML_ file
    ```bash
    kubectl create -f pod-definition.yml
    ```
* Create a _Pod_ based on _YAML_ file and record changes
    ```bash
    kubectl create -f pod-definition.yml --record
    ```
* Also, we can use the `apply` command:
    ```bash
    kubectl apply -f pod-definition.yml
    ```
* We can edit a _Pod_ using the `edit` command:
```bash
kubectl edit pod nginx-app
```
* Delete a _Pod_
   ```bash
   kubectl delete pod nginx
   ```

## Kubernates Controllers
### ReplicationController
* YAML definition file example
    ```yml
    apiVersion: v1
    kind: ReplicationController
    metadata:
    name: myapp-rc
    labels:
        app: myapp
        type: front-end
    spec:
    template:
        metadata:
        name: myapp-pod
        labels:
            app: myapp
            type: front-end
        spec:
        containers:
            - name: nginx-container
            image: nginx
    replicas: 3
    ```
* Create Replication Controller based on YAML file
    ```bash
    kubectl create -f rc-definition.yml
    ```
* List Replication Controllers
    ```bash
    kubectl get replicationcontroller
    ```
* Delete Replication Controller
    ```bash
    # Also delete underlying PODs
    kubectl get replicationcontroller myapp-replicationcontroller
    ```
### ReplicaSet
* YAML definition file example
    ```yml
    apiVersion: apps/v1
    kind: ReplicaSet
    metadata:
    name: myapp-replicaset
    labels:
        app: myapp
        type: front-end
    spec:
    template:
        metadata:
        name: myapp-pod
        labels:
            app: myapp
            type: front-end
        spec:
        containers:
            - name: nginx-container
            image: nginx
    replicas: 3
    selector:
        matchLabels:
        type: front-end
    ```
* Create Replica Set based on YAML file
    ```bash
    kubectl create -f replicaset-definition.yml
    ```
* List Replica Sets
    ```bash
    kubectl get replicaset
    ```
* Delete Replica Set
    ```bash
    # Also delete underlying PODs
    kubectl get replicaset myapp-replicaset
    ```
### Scale ReplicaSet
* When the definition file is available
    ```bash
    kubectl replace -f replicaset-definition.yml
    ```
* To change the number of `replicas` with reference to the definition file
    ```bash
    kubectl scale --replicas=6 -f replicaset-definition.yml
    ```
* To change the number of `replicas` with reference to the replica set name
    ```bash
    kubectl scale --replicas=6 replicaset myapp-replicaset
    ```
    * **TYPE**: replicaset
    * **NAME**: name of the replica set

## Deployment
* Create a deployment based on YAML file with `--record` option
    ```bash
    kubectl create -f ./deployment-definition.yml --record
    ```

[<<< Back to Home](./README.md)