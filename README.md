# GitHub Actions Controller (ARC) with Kind

This repo is an example of running ARC and GitHub Workflows that require `docker`
command (e.g. they build docker images).

Create Kubernetes Cluster:
```bash
kind create cluster
```

Deploy Cert Manager:
```bash
kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.8.2/cert-manager.yaml
```

Deploy and Configure ARC:
```bash
kubectl create -f \
    https://github.com/actions/actions-runner-controller/\
    releases/download/v0.27.3/actions-runner-controller.yaml

kubectl create secret generic controller-manager \
    -n actions-runner-system \
    --from-literal=github_token=YOUR_PERSONAL_ACCESS_TOKEN_WITH_REPO_SCOPE
```

Create Self-Hosted Runner:
```bash
kubectl apply -f runner-deployment.yaml
```

GitHub runner should now show on the runners' list for the configured repository.
Trigger the workflow manually to test the setup.

Delete Cluster:
```bash
kind delete cluster
```
