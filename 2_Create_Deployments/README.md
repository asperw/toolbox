## Deployments

* Deployments allow you to specify the number of replicas of a container
* You can generate a deployment with `k create deployment mydep --image=nginx --replicas=3 --dry-run=client -o yaml > mydep.yaml`
* Simulate a failed rollout by first deploying the successful deployment with `kubectl apply -f successful.yaml` and then rollout the failed deployment with `kubectl apply -f simulatefail.yaml`

You can watch deployments rolling out with `watch -n "kubectl get pods"`
