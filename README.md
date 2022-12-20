# Crossplane demonstration

This is a small demonstration project for deploying a VPC and an EC2 instance on AWS using [Crossplane](https://github.com/crossplane/crossplane).

## Install Crossplane inside Kubernetes Cluster

```bash
helm repo add crossplane-stable https://charts.crossplane.io/stable
helm repo update
helm install crossplane --namespace crossplane-system --create-namespace crossplane-stable/crossplane
```
see https://docs.crossplane.io/v1.10/getting-started/install-configure/ for more details

## Install Crossplane CLI

```bash
curl -sL https://raw.githubusercontent.com/crossplane/crossplane/master/install.sh | sh
```

## Create Secrets for accessing Provider
