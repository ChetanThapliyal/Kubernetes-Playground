# Basic commands for Pods using `kubectl`

Here are some basic `kubectl` commands for managing Pods in Kubernetes, along with examples:

1. **Create a Pod**: Use the `kubectl create` command ***to create a Pod from a YAML or JSON file***.
    
    ```bash
    kubectl create -f pod.yaml
    #OR
    kubectl run my-pod --image=my-image --port=8080
    ```
    
    
    💡 The `kubectl create` and `kubectl run` commands in Kubernetes are used for different purposes:
    
    - **`kubectl create`**: The `kubectl create` command is used to create resources in Kubernetes based on a YAML or JSON file. It is a general-purpose command for creating various Kubernetes objects, including Pods, Deployments, Services, ConfigMaps, and more.
        
        Example:
        
        ```
        kubectl create -f pod.yaml
        ```
        
        In the example above, a Pod is created using the YAML file `pod.yaml`. The file contains the definition of the Pod object, specifying its metadata, containers, volumes, and other properties.
        
    - **`kubectl run`**: The `kubectl run` command is primarily used for quickly creating a Pod or a Deployment. It is commonly used for running a one-off or ephemeral Pod for tasks like running a container for testing, troubleshooting, or executing a short-lived job.
        
        Example:
        
        ```
        kubectl run my-pod --image=my-image --port=8080
        ```
        
        In the example above, a Pod is created using the `kubectl run` command. It specifies the name of the Pod (`my-pod`), the container image to run (`my-image`), and the container's listening port (`8080`).
        
        It's important to note that the `kubectl run` command can also be used to create Deployments instead of Pods by providing additional flags, such as `--replicas` and `--labels`. This makes it convenient for quickly creating a Deployment and managing multiple replicas of a Pod.
        ***
        > Basically, while both `kubectl create` and `kubectl run` can be used to create Pods, `kubectl create` is a more general-purpose command used for creating various Kubernetes resources, while `kubectl run` is primarily used for quickly creating a single Pod or Deployment, especially for ephemeral or one-off tasks.

    
2. **Get Pods**: Use the `kubectl get pods` command ***to list all the Pods in the current namespace***.
    
    ```bash
    kubectl get pods
    ```
    
3. **Describe a Pod**: Use the `kubectl describe pod` command ***to get detailed information about a specific Pod***.
    
    ```
    kubectl describe pod my-pod
    ```
    
4. **Delete a Pod**: Use the `kubectl delete pod` command ***to delete a Pod by its name***.
    
    ```
    kubectl delete pod my-pod
    ```
    
5. **Logs of a Pod**: Use the `kubectl logs` command ***to fetch the logs of a specific Pod***.
    
    ```
    kubectl logs my-pod
    ```
    
6. **Exec into a Pod**: Use the `kubectl exec` command ***to execute a command inside a running Pod***.
    
    ```
    kubectl exec -it my-pod -- bash
    ```
    
7. **Port Forwarding**: Use the `kubectl port-forward` command to ***forward a local port to a port on a Pod***.
    
    ```
    kubectl port-forward my-pod 8080:80
    ```
    
8. **Scaling Pods**: Use the `kubectl scale` command ***to scale the number of replicas of a Deployment***, which indirectly scales the Pods.
    
    ```
    kubectl scale deployment my-deployment --replicas=3
    ```
    
9. **Pod Events**: Use the `kubectl get events` command to ***view the events associated with Pods***.
    
    ```
    kubectl get events --field-selector involvedObject.kind=Pod
    ```
    
10. **Pod Status**: Use the `kubectl get pods` command with the `o wide` option to ***see additional information about the Pods***, including their current status, IP address, and node.
    
    ```
    kubectl get pods -o wide
    ```
    

## Pods with YAML

- Kubernetes uses YAML files as input for the creation of objects such as PODs, Replicas, Deployments, Services etc.
- A kubernetes definition file always contains 4 top level fields (or root level properties).
    - **ApiVersion :** specifies the version of the Kubernetes API to use
    - **Kind :** specifies the Kubernetes resource type. Here, it is set to `Pod`
    - **Metadata :** provides metadata about the Pod, including its name. In this example, the Pod is named `my-pod`.
    - **Spec :** defines the desired specification of the Pod.
        - The `containers` field lists the containers to run within the Pod. In this example, there is one container defined.
        - Each container within the `containers` list has a `name` and an `image` specified. The `name` is used to identify the container, and the `image` specifies the container image to run. In this case, the Pod runs an nginx container with the `latest` tag.
- These are all REQUIRED fields, so you MUST have them in your configuration file.

To create the Pod using this YAML file, you can use the `kubectl create` command:

```bash
kubectl create -f pod.yaml
```

This command reads the YAML file and creates the Pod as defined.

You can also use the `kubectl apply` command to create or update a Pod based on the YAML file:

```bash
kubectl apply -f pod.yaml
```

If the Pod does not exist, it will be created. If it already exists, any changes made to the YAML file will be applied to the existing Pod.

Once the Pod is created, you can use various `kubectl` commands to interact with it, such as `kubectl get pods`, `kubectl describe pod`, `kubectl logs`, and more.