## Create clsuter

```bash
eksctl create cluster --name self-hosted --region ap-southeast-1 --nodegroup-name self-hosted-workers --node-type t3.medium --nodes 1 --nodes-min 1 --nodes-max 2 --managed
```

## Update kubeconfig

```bash
aws eks --region ap-southeast-1 update-kubeconfig --name self-hosted
```

## Verify cluster

```bash
kubectl get nodes
```

## Install cert-manager

```bash
helm install cert-manager jetstack/cert-manager --namespace cert-manager --create-namespace --version v1.16.1 --set crds.enabled=true

```

## Verify cert-manager

```bash
kubectl get pods -n cert-manager
```

## Create Secret 

```bash
## Create namspace for actions-runner-system
kubectl create ns actions-runner-system

## Create secret in actions-runner-system namespace
kubectl create secret generic controller-manager -n actions-runner-system --from-literal=github_token=<GITHUB-PAT>

```

## Install Action Runner Controller

```bash
## Add the Actions Runner Controller Helm repository
helm repo add actions-runner-controller https://actions-runner-controller.github.io/actions-runner-controller

## Update the Helm repository
helm repo update

## Install Actions Runner Controller
helm upgrade --install --namespace actions-runner-system --wait actions-runner-controller actions-runner-controller/actions-runner-controller -f values.yaml

```

## Verify Action Runner Controller

```bash
kubectl get pods -n actions-runner-system
```

