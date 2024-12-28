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
* Get in a pod with `k exec -it mypod -c mycontainer -- /bin/bash`
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

## Networking

* Pods are ephemeral
* Pods are assigned ip addresses
* You can expose a single pod with `k port-forward -n myns pods/mypod-1234567890-abdce 9000`
* Containers can communicate on the pod level
* Find the networking plugin used by the cni in rancher desktop with
  * `rdctl shell bash`
  * Find the conf in `/etc/cni` with `tree`

## Services

* Services provide a single entrypoint to a group of pods
* You can create a service manually with `k expose deployment mydep --port 9000`
* When a service is created it creates a name that is resolvable in the dns of the cluster
* A loadbalancer service doesn't require exposing a port to reach the deployment

## Ingress
* Exposes http/s from a service
* Provides ssl/tls termination
* Ingress controllers
  * Traefik
  * Nginx
  * Cloud provider specific

## Storage
* Types of volumes
  * emptydir
    * Initially empty
    * All containers in pod can read and write
    * Scratch space
* Containers must mount the volumes
* Persistent volume claim
  * Have lifecycle independent of pod
* Storage classes
  * local-path
  * aws ebs
  * vsphere
  * nfs
* Access modes
  * Read write once
    * Available only on the node
    * Forces scheduler to put all pods that need this volume here
  * Read write many
    * All nodes can access

## K9s

* Vim keybinds
* Use `shift+a` to sort by age
* Use `shift+s` to sort by status
