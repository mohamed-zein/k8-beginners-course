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
* YAML Definition file example
    ```yml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
    name: myapp-deployment
    labels:
        tier: frontend
        app: nginx
    spec:
    selector:
        matchLabels:
        app: myapp
    replicas: 6
    template:
        metadata:
        name: nginx-2
        labels:
            app: myapp
        spec:
        containers:
        - name: nginx
            image: nginx
    ```
* Create a Deployment based on a YAML definition file
    ```bash
    kubectl create -f deployment-definition.yml
    ```
* Create a deployment based on YAML file with `--record` option
    ```bash
    kubectl create -f ./deployment-definition.yml --record
    ```
* List Deployments
    ```bash
    kubectl get deployments
    ```
* Deployments will automatically create a ReplicaSet
    ```bash
    kubectl get replicaset
    ```
* List all objects
    ```bash
    kubectl get all
    ```
* Describe a deployment
    ```bash
    kubectl describe deployment myapp-deployment
    ```
### Rollout command
* Rollout Status
    ```bash
    kubectl rollout status deployment/myapp-deployment
    ```
* Rollout History
    ```bash
    kubectl rollout history deployment/myapp-deployment
    ```
### Update a deployment
* Update a deployment using deployment file
    ```bash
    kubectl apply -f ./deployment-definition.yml
    ```
* Update only the image of a deployment on the fly
    ```bash
    kubectl set image deployment/myapp-deployment nginx=nginx:1.23
    ```
### Rollback
* Rollback a deployment to a previous _Revision_.
    ```bash
    kubectl rollout undo deployment/myapp-deployment
    ```

[<<< Back to Home](./README.md)