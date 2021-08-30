# Komodor's Agent

## Installation

!!! Note ""
    Before installing the agent, get your API key from the Integration page

![API Key Location](./img/api_key_location.png)

### Kustomize

```bash
export KOMOKW_API_KEY= # API KEY Required
export KOMOKW_CLUSTER_NAME= # Optional
kubectl create ns komodor
kubectl apply -n komodor -k https://github.com/komodorio/helm-charts/manifests/overlays/full/?ref=master
```
### Helm

```bash
helm repo add komodorio https://helm-charts.komodor.io
helm repo update
helm upgrade --install k8s-watcher komodorio/k8s-watcher \
 --set apiKey=YOUR_API_KEY_HERE \
 --set watcher.clusterName=CLUSTER_NAME \
 --set watcher.enableAgentTaskExecution=true \
 --set watcher.allowReadingPodLogs=true

```

## Permissions
Komodor's Agents uses native RBAC model of Kubernetes. All the permissions listed here:

1. [helm](https://github.com/komodorio/helm-charts/blob/master/charts/k8s-watcher/templates/clusterrole.yaml)
2. [kustomize base](https://github.com/komodorio/helm-charts/blob/master/manifests/base/clusterrole.yaml), [kustomize final](https://github.com/komodorio/helm-charts/blob/master/manifests/overlays/full/logs-reader.cr.yaml)


## ARM Support

* linux/amd64
* linux/arm64 (v8) - starting from agent version 0.1.29

The default is linux/amd64. If you wish to install the chart for linux/arm64 all you need to do is set image.arm flag. For example: `--set image.arm=true`

## Advanced Configuration


## Uninstalling

### Kustomize
```bash
kubectl delete ns komodor
```

### Helm
```bash
helm uninstall k8s-watcher
```
