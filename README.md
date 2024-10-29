# ArgoCD

# Argo CD Administration Guide

This guide provides step-by-step instructions on installing, configuring, and managing applications with Argo CD in a Kubernetes cluster.

## Prerequisites
- A running Kubernetes cluster (Minikube, EKS, GKE, or AKS).
- `kubectl` CLI and `argocd` CLI tools installed.

## 1. Installing Argo CD

1. **Install Argo CD** in the `argocd` namespace:
```bash
   kubectl create namespace argocd
   kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```
## Credetials 
```bash
kubectl get secret argocd-initial-admin-secret -n argocd -o jsonpath="{.data.password}" | base64 -d
```

## Login to Argo CD
```bash 
argocd login localhost:8080 --username admin --password <default_password>
```

#  Setting Up Git Repository and Creating an Application
## 1. Add a Git Repository:
```bash
argocd repo add https://github.com/<your-username>/<your-repo> --username <your-username> --password <your-password>
```
 ## 2. Create an Application:
 ```bash
 argocd app create demo-app \
  --repo https://github.com/<your-username>/<your-repo> \
  --path <path-to-k8s-manifests> \
  --dest-server https://kubernetes.default.svc \
  --dest-namespace default
```
## 3. Sync the Application
```bash
argocd app sync demo-app
```
