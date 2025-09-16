## Create KinD Cluster

```bash
kind create cluster --name traefik-demo --config kind-config.yaml
```

## Required CRD for Traefik 

```bash
kubectl apply -f https://raw.githubusercontent.com/traefik/traefik/v3.0/docs/content/reference/dynamic-configuration/kubernetes-crd-definition-v1.yml
```

This will create the necessary CRDs for Traefik to work with Kubernetes.

## Install Traefik related resources

```bash
kubectl apply -f base/traefik
```

## Accessing the Traefik Dashboard

```bash
localhost:9000/dashboard/
```

## Install Sample Application

```bash
kubectl apply -f base/bookstore     
```

## Accessing the Sample Application

```bash
localhost
```

## Cluster Cleanup

```bash
kind delete cluster --name traefik-demo
```
