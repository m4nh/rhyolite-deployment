# Rhyolite Deployment GitOps Repository

This is a GitOps repository for deploying Rhyolite using ArgoCD. It contains the necessary Kubernetes manifests and configurations to set up Rhyolite in a Kubernetes cluster.

You can pull this repository and -- insanely -- deploy it with simple kubectl commands. Or, better yet, use ArgoCD to manage the deployment and lifecycle of Rhyolite.


## Install ArgoCD

Create namespace and install ArgoCD using the stable manifest:

```bash
# 1. Create the namespace
kubectl create namespace argocd

# 2. Apply the stable manifest
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

Forward the ArgoCD server port to localhost (and access it at https://localhost:8080):

```bash
kubectl port-forward svc/argocd-server -n argocd 8080:443
```

Retrieve the initial admin password:

```bash
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
```
