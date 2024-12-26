# toolbox

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
* Can be edited with `k edit pod`

## Manifests

* You can generate a manifest with `k run nginx-yaml --image=nginx --dry-run=client -o yaml > nginx.yaml`
* You can update pods by applying manifests `k apply -f nginx-yaml.yaml`
