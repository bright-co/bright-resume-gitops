# Bright Resume GitOps Setup

![Bright Resume Logo](https://raw.githubusercontent.com/ErfanSeidipoor/bright-resume/development/libs/assets/src/image/logo-with-typography-horizontal-light.png)

[![License](https://img.shields.io/github/license/your_username/resume-builder.svg?style=flat-square)](https://github.com/bright-co/bright-resume-gitops/blob/main/LICENSE)
[![GitHub issues](https://img.shields.io/github/issues/ErfanSeidipoor/bright-resume)](https://github.com/bright-co/bright-resume-gitops/issues)
[![GitHub stars](https://img.shields.io/github/stars/ErfanSeidipoor/bright-resume)](https://github.com/bright-co/bright-resume-gitops/stargazers)
## Overview
This repository contains the GitOps setup for deploying and managing [Your Open Source Project] on Kubernetes using ArgoCD.

## Table of Contents
- [Prerequisites](#prerequisites)
- [Setting Up the Kubernetes Cluster](#setting-up-the-kubernetes-cluster)
- [Folder Structure](#folder-structure)
- [Contributing](#contributing)
- [License](#license)

## Prerequisites
Ensure you have the following tools installed:
- `kubectl`: Kubernetes command-line tool
- `argocd`: ArgoCD command-line tool


## Setting Up the Kubernetes Cluster
Make sure your Kubernetes cluster is set up and configured correctly. Execute the following commands to prepare the cluster:

```bash

# Installing ingress-nginx
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.9.4/deploy/static/provider/cloud/deploy.yaml


# Creating namespace for each environment
kubectl create namespace development
kubectl create namespace staging
kubectl create namespace production

# Creating namespace for minio
kubectl create namespace minio

## Creating secrets 
kubectl create secret generic minio-password --from-literal=password=<****> -n=minio

kubectl create secret generic mongo-resume-password --from-literal=password=<****> -n=development
kubectl create secret generic mongo-auth-password --from-literal=password=<****> -n=development
kubectl create secret generic mongo-file-password --from-literal=password=<****> -n=development
kubectl create secret generic postgres-cms-password --from-literal=password=<****> -n=development
kubectl create secret generic jwt-secret --from-literal=secret=<****> -n=development
kubectl create secret generic minio-password --from-literal=password=$(kubectl get secret --namespace minio minio-password -o jsonpath="{.data.password}" | base64 --decode) -n=development


kubectl create secret generic cms-keys --from-literal=keys=<****>,<****>,<****>,<****>  -n=development
kubectl create secret generic cms-token-salt --from-literal=salt=<****> -n=development
kubectl create secret generic cms-admin-jwt-secret --from-literal=secret=<****> -n=development
kubectl create secret generic cms-transfer-token-salt --from-literal=salt=<****> -n=development
kubectl create secret generic cms-jwt-secret --from-literal=secret=<****> -n=development
kubectl create secret generic cms-api-token-salt --from-literal=salt=<****> -n=development


kubectl create secret generic mongo-resume-password --from-literal=password=<****> -n=staging
kubectl create secret generic mongo-auth-password --from-literal=password=<****> -n=staging
kubectl create secret generic mongo-file-password --from-literal=password=<****> -n=staging
kubectl create secret generic postgres-cms-password --from-literal=password=<****> -n=staging
kubectl create secret generic jwt-secret --from-literal=secret=<****> -n=staging
kubectl create secret generic minio-password --from-literal=password=$(kubectl get secret --namespace minio minio-password -o jsonpath="{.data.password}" | base64 --decode) -n=staging

kubectl create secret generic cms-keys --from-literal=keys=<****>,<****>,<****>,<****>  -n=staging
kubectl create secret generic cms-token-salt --from-literal=salt=<****> -n=staging
kubectl create secret generic cms-admin-jwt-secret --from-literal=secret=<****> -n=staging
kubectl create secret generic cms-transfer-token-salt --from-literal=salt=<****> -n=staging
kubectl create secret generic cms-jwt-secret --from-literal=secret=<****> -n=staging
kubectl create secret generic cms-api-token-salt --from-literal=salt=<****> -n=staging


kubectl create secret generic mongo-resume-password --from-literal=password=<****> -n=production
kubectl create secret generic mongo-auth-password --from-literal=password=<****> -n=production
kubectl create secret generic mongo-file-password --from-literal=password=<****> -n=production
kubectl create secret generic postgres-cms-password --from-literal=password=<****> -n=production
kubectl create secret generic jwt-secret --from-literal=secret=<****> -n=production
kubectl create secret generic minio-password --from-literal=password=$(kubectl get secret --namespace minio minio-password -o jsonpath="{.data.password}" | base64 --decode) -n=production

kubectl create secret generic cms-keys --from-literal=keys=<****>,<****>,<****>,<****>  -n=production
kubectl create secret generic cms-token-salt --from-literal=salt=<****> -n=production
kubectl create secret generic cms-admin-jwt-secret --from-literal=secret=<****> -n=production
kubectl create secret generic cms-transfer-token-salt --from-literal=salt=<****> -n=production
kubectl create secret generic cms-jwt-secret --from-literal=secret=<****> -n=production
kubectl create secret generic cms-api-token-salt --from-literal=salt=<****> -n=production

# Installing Cert Manager
kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.13.3/cert-manager.yaml

# Creating persistance volume for minio
kubectl apply -f ./minio/persistent-volume.yaml

# Creating minio
kubectl apply -f ./minio/minio.yaml
kubectl apply -f ./minio/ingress.yaml

# Creating persistance volume for each environment
kubectl apply -f ./development-pv/persistent-volume-mongo-file.yaml
kubectl apply -f ./development-pv/persistent-volume-mongo-auth.yaml
kubectl apply -f ./development-pv/persistent-volume-mongo-resume.yaml
kubectl apply -f ./development-pv/persistent-volume-postgres-cms.yaml

kubectl apply -f ./staging-pv/persistent-volume-mongo-file.yaml
kubectl apply -f ./staging-pv/persistent-volume-mongo-auth.yaml
kubectl apply -f ./staging-pv/persistent-volume-mongo-resume.yaml
kubectl apply -f ./staging-pv/persistent-volume-postgres-cms.yaml

kubectl apply -f ./production-pv/persistent-volume-mongo-file.yaml
kubectl apply -f ./production-pv/persistent-volume-mongo-auth.yaml
kubectl apply -f ./production-pv/persistent-volume-mongo-resume.yaml
kubectl apply -f ./production-pv/persistent-volume-postgres-cms.yaml

# Installing ArgoCD
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
kubectl apply -f ./minio/ingress.yaml

## Creating ArgoCD applications
kubectl apply -f ./argocd/argocd.development.yaml
kubectl apply -f ./argocd/argocd.staging.yaml
kubectl apply -f ./argocd/argocd.production.yaml
```


## Folder Structure
The project follows a structured organization for different environments:

- `development/`: Contains manifest files for the development environment.
- `staging/`: Contains manifest files for the staging environment.
- `production/`: Contains manifest files for the production environment.


## Contributing
We welcome contributions from the open-source community!

## License
This project is licensed under the [Your License] - see the LICENSE.md file for details.
