# toolbox

These notes were gathered by following courses on udemy and self paced workshops on aws

## Setup rancher desktop

* Use moby container engine
* Make sure context is rancher-desktop not docker-desktop
* Make sure kubernetes is not running in docker desktop
* Docker desktop conflicts with rancher desktop despite appearing to run well together
* Make sure docker desktop does not start at login
* Use the `kubectl` plugin with oh my zsh for autocompletion and aliases

## Cluster

* A cluster has a control plane and nodes that contain pods
* The control plane has
  * Etcd (the brain)
  * Scheduler
    * Fulfills requests from api server by assigning pods to nodes
  * Api server (6443)
    * Kubectl reads config in `~/.kube/config` to find api server
* Nodes have
  * One or more pods
    * One or more containers

## Pods

* Pods have one or more containers
* Storage
  * Several containers can use the same storage
* Can be edited with `k edit pod mypod`
* Get in a pod with `k exec -it mypod -- /bin/bash`
  * What shell and executables are available depends on the image

## Manifests

* You can generate a manifest with `k run mypod --image=nginx --dry-run=client -o yaml > mypod.yaml`
* You can update pods by applying manifests `k apply -f mypod.yaml`

## Deployments

* Deployments allow you to specify the number of replicas of a container
* You can generate a deployment with `k create deployment mydep --image=nginx --replicas=3 --dry-run=client -o yaml > mydep.yaml`
* Deployments have strategies to update container versions

## Namespaces
* If you give no indication of namespace like using `--namespace myns` or `-n myns` in commands then it will use the default namespace
* You can choose the current working namespace with `kubectl config set-context --current --namespace=myns`
