# Crossplane demonstration

## Install Crossplane inside Kubernetes Cluster

```bash
helm repo add crossplane-stable https://charts.crossplane.io/stable
helm repo update
helm install crossplane --namespace crossplane-system --create-namespace crossplane-stable/crossplane
```
see https://docs.crossplane.io/v1.10/getting-started/install-configure/ for more details
