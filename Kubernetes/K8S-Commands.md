These commands represent a common workflow for practicing Kubernetes, from setting up a local cluster to deploying various object types.

## Initial Setup and Cluster Creation

The first set of commands focuses on setting up a local Kubernetes cluster using Kind (Kubernetes in Docker).
```bash
mv /home/ubuntu/config.yml /home/ubuntu/kind-cluster: This command moves a file named config.yml from one directory to another.

ls: Lists the contents of the current directory.
```
```bash
o	git clone https://github.com/komal-sketch/Kubernetes.git
```

o	mkdir KIND-project: Creates a new directory named KIND-project.

o	cd KIND-Project: Changes the current directory to the newly created KIND-project folder.

o	vim config.yml: Opens the config.yml file in the Vim text editor to edit the Kind cluster configuration.

```bash
o	kind create cluster --name=tws-cluster --config=config.yml: Creates a new Kind cluster named K8s-cluster using the specified configuration file.
```

## Cluster and Resource Inspection

This section involves using kubectl to inspect the cluster and its components.

This command displays information about the tws-cluster, confirming its status and API server endpoint:
```bash
kubectl cluster-info --context kind-tws-cluster
```

Lists the nodes (virtual machines) in the cluster.
```bash
kubectl get nodes
```

Runs the kubectl get nodes command repeatedly, allowing you to monitor the state of the nodes in real-time.
```bash
watch kubectl get nodes
```

Lists all namespaces in the cluster.
```bash
kubectl get ns or kubectl get namespaces
```

Lists the pods. The -n flag is used for specifying a namespace for namespaced resources like pods, not cluster-scoped resources like nodes.
```bash
kubectl get pods -n kube-system
```

Lists all pods in the current namespace (by default, default).
```bash
kubectl get pods
```
## Deploying a Pod with kubectl run and kubectl apply

These commands demonstrate two ways of deploying a pod: using a command-line shortcut and using a YAML file.




