## Manifests

* You can generate a manifest with `k run nginx-yaml --image=nginx --dry-run=client -o yaml > nginx.yaml`
* You can update pods by applying manifests `k apply -f nginx-yaml.yaml`
