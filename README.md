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

# Installing ArgoCD
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

# Creating namespace for each environment
kubectl create namespace development
kubectl create namespace staging
kubectl create namespace production

# Creating persistance volume for each environment
kubectl apply -f ./development-pv/persistent-volume-mongo-file.yaml

## creating secrets
kub create secret generic mongo-resume-password --from-literal=password=<YOUR_PASSWORD> -n=development
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
