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

### This command displays information about the tws-cluster, confirming its status and API server endpoint:
```bash
kubectl cluster-info --context kind-tws-cluster
```

### Lists the nodes (virtual machines) in the cluster.
```bash
kubectl get nodes
```

### Runs the kubectl get nodes command repeatedly, allowing you to monitor the state of the nodes in real-time.
```bash
watch kubectl get nodes
```

### Lists all namespaces in the cluster.
```bash
kubectl get ns or kubectl get namespaces
```

### Lists the pods. The -n flag is used for specifying a namespace for namespaced resources like pods, not cluster-scoped resources like nodes.
```bash
kubectl get pods -n kube-system
```

### Lists all pods in the current namespace (by default, default).
```bash
kubectl get pods
```
## Deploying a Pod with kubectl run and kubectl apply

These commands demonstrate two ways of deploying a pod: using a command-line shortcut and using a YAML file.

### Creates a new namespace called nginx.
```bash
kubectl create ns nginx
```
### Lists all namespaces to confirm the creation.
```bash
kubectl get ns
```
### This command creates a pod named nginx from the nginx image within the nginx namespace. This is a quick way to create a single pod.
```bash
kubectl run nginx --image=nginx -n nginx
```
### Deletes the pod named nginx in the nginx namespace.
```bash
kubectl delete pod nginx -n nginx
```
### Deletes the entire nginx namespace.
```bash
kubectl delete ns nginx
```
### Opens a YAML file to define a namespace, which is a more declarative way to manage resources.
```bash
vim namspace.yml
```
### Applies the configuration from the YAML file, creating the namespace.
```bash
kubectl apply -f namspace.yml
```
### This command executes a bash shell inside a running pod named nginx-pod in the nginx namespace. The -it flags stand for interactive and TTY, allowing you to interact with the shell.
```bash
kubectl exec -it nginx-pod -n nginx -- bash
```

## Deployments, Scaling, and Updates
This section focuses on Deployments, which are a higher-level abstraction for managing replicated pods.

### This command scales the number of pods in the Deployment to 5.
```bash
kubectl scale deployment nginx-deployment -n nginx --replicas=5
```
### This command updates the Docker image of the pods managed by the Deployment to version
```bash
kubectl set image deployment/nginx-deployment -n nginx nginx=nginx:1.29.1
```
## Other Kubernetes Object Types
This part explores other workload object types beyond Deployments.

### Copies the Deployment YAML file to a new file for a ReplicaSet.
```bash
cp deployment.yml replicasets.yml
```
### Edits the copied file to change the kind from Deployment to ReplicaSet. A ReplicaSet ensures a specified number of pod replicas are running at all times.
```bash
vim replicasets.yml
```
### Creates the ReplicaSet.
```bash
kubectl apply -f replicasets.yml
```
### Copies the ReplicaSet file to a new file for a DaemonSet.
```bash
cp replicasets.yml daemonsets.yml
```
### Edits the file to change the kind to DaemonSet. A DaemonSet ensures that a copy of a pod is running on every node in the cluster.
```bash
vim daemonsets.yml
```
### Opens a YAML file for a Job. A Job creates one or more pods and ensures that a specified number of them successfully terminate.
```bash
vim jobs.yml
```
### Creates the Job.
```bash
kubectl apply -f jobs.yml
```
### Retrieves the logs from the Job pod.
```bash
kubectl logs pod/demo-job-hlz8s -n nginx
```
### Opens a YAML file for a CronJob. A CronJob creates Jobs on a repeating schedule.
```bash
vim cronjob.yml
```
## Final Commands and Cleanup
The last few commands involve a cleanup and checking all resources.

### This is a very useful command that lists all resources in a given namespace, including pods, services, deployments, and more.
```bash
kubectl get all -n nginx
```
### This command forwards network traffic from a local port (81) to a port on a Kubernetes service (80). This makes the service 
accessible from your local machine. The sudo -E is used for elevated privileges, 
and --address=0.0.0.0 makes the forwarded port accessible from outside the local machine (e.g., in a cloud environment).
```bash
sudo -E kubectl port-forward service/nginx-service -n nginx 81:80 --address=0.0.0.0
```


