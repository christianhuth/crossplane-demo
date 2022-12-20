# Crossplane demonstration

This is a small demonstration project for deploying a VPC and an EC2 instance on AWS using [Crossplane](https://github.com/crossplane/crossplane).

# Basic Setup of the Crossplane Environment

see https://docs.crossplane.io/v1.10/getting-started/install-configure/ for more details

## Install Crossplane inside Kubernetes Cluster

```bash
helm repo add crossplane-stable https://charts.crossplane.io/stable
helm repo update
helm install crossplane --namespace crossplane-system --create-namespace crossplane-stable/crossplane
```

## Install Crossplane CLI

```bash
curl -sL https://raw.githubusercontent.com/crossplane/crossplane/master/install.sh | sh
```

# Setup for our Demonstration on AWS

## Install AWS Provider

### Using the CLI

```bash
# default method using the provided package
kubectl crossplane install provider xpkg.upbound.io/crossplane-contrib/provider-aws:v0.34.0
# alternative method using the docker image
# kubectl crossplane install provider crossplane/provider-aws:v0.34.0
```

### Using the Template

```bash
kubectl apply -f templates/provider.yaml
```

## Create Secrets for accessing Provider
