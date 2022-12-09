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

## kubectl 
* Check cluster info
    ```bash
    kubectl cluster-info
    ```
* List nodes of the cluster
    ```bash
    kubectl get nodes
    ```
* Run a _Pod_ based on an image
    * Name: nginx-app
    * Image: nginx
    ```bash
    kubectl run nginx-app --image nginx
    ```
    * An alternative is to use option `-o yaml` to run a _Pod_ and **output** the YAML file
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
* Create a _Pod_ based on _YAML_ file

    ```bash
    kubectl create -f pod-definition.yml
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