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

⚠️ Setting up AWS CLI is not part of this demonstration. ⚠️

## Install AWS Provider

See [here](https://marketplace.upbound.io/providers/crossplane-contrib/provider-aws/v0.34.0) for complete Docs about Provider.

### Using the CLI

```bash
# default method using the provided package
kubectl crossplane install provider xpkg.upbound.io/crossplane-contrib/provider-aws:v0.34.0
```

### Using the Template

```bash
kubectl apply -f templates/provider.yaml
```

## Check the installed Provider

```bash
kubectl get providers
kubectl describe providers crossplane-contrib-provider-aws
```

As soon as the Provider is healthy you can check the provided CRDs:

```bash
kubectl api-resources | grep aws
```

## Create Secrets for accessing Provider

```bash
AWS_PROFILE=default && echo -e "[default]\naws_access_key_id = $(aws configure get aws_access_key_id --profile $AWS_PROFILE)\naws_secret_access_key = $(aws configure get aws_secret_access_key --profile $AWS_PROFILE)" > creds.conf

kubectl create secret generic crossplane-demo-aws-credentials -n crossplane-system --from-file=creds=./creds.conf
```

## Configure the Provider

```bash
kubectl apply -f templates/providerconfig.yaml
```
