# Kubernetes Concepts - PODs, ReplicaSets, Deployment

This section is about creating a POD using a YAML based configuration file.

* Kubernetes uses YAML files as input for the creation of objects such as PODs, Replicas, Deployments, Services etc.
* A kubernetes definition file always contains 4 top level fields. These are all **REQUIRED** fields, so you **MUST** have them in your configuration file
1. `apiVersion`: This is the version of the kubernetes API we’re using to create the object. Depending on what we are trying to create we must use the **RIGHT** `apiVersion`
    * For now since we are working on PODs, we will set the `apiVersion` as `v1`.
2. `kind`: refers to the type of object we are trying to create, which in this case happens to be a POD. 
    * Other possible values here could be `ReplicaSet` or `Deployment` or `Service`:
        Kind | Version
        -----|--------
        POD | v1
        Service | v1
        ReplicaSet | apps/v1
        Deployment | apps/v1
3. `metadata`: is data about the object like its name, labels etc. 
    * It’s **IMPORTANT** to note that under metadata, you can only specify name or labels or anything else that kubernetes expects to be under metadata. 
    * You **CANNOT** add any other property as you wish under this. However, under labels you **CAN** have any kind of key or value pairs as you see fit. 
    * So it's **IMPORTANT** to understand what each of these parameters expect.
4. `spec`: object we are going to create, this is were we provide additional information to kubernetes pertaining to that object. 
    * This is going to be different for different objects, so its important to understand or refer to the documentation section to get the right format for each.

In the [example](./code-example/pod-definition.yml), the YAML file descibes a POD which contain single container of `nginx` image.

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

## Commands 
* Once the file is created, run the command `kubectl create -f` followed by the file name which is _pod-definition.yml_ and kubernetes creates the pod.

    ```bash
    kubectl create -f pod-definition.yml
    ```

* To check running pods:

    ```bash
    kubectl get pods
    ```

* To get details of **myapp-pod** pod

    ```bash
    kubectl describe pod myapp-pod
    ```

[<<Previous](../unit05-yaml-introduction/README.md) | [Next>>]()