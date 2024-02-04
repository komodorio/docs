# The Komodor Agent

## Permissions

The Komodor agent uses the native RBAC model of Kubernetes. All the permissions are listed here:

1. [helm](https://github.com/komodorio/helm-charts/blob/master/charts/k8s-watcher/templates/clusterrole.yaml)

## ARM Support

Arm64 image is supported via docker manifest. 

## Advanced Configuration

You can configure the agent's functionality using the following configuration file: `komodor-k8s-watcher.yaml` (assuming the RBAC permissions are satisfied).
A more detailed list of the configurable parameters can be found [here](https://github.com/komodorio/helm-charts/tree/master/charts/k8s-watcher#configuration)

### Data Redaction

Learn how to set up [data redaction](./Sensitive-Information-Redaction.md) in Komodor

### Resources

By default, the Komodor agent watches the majority of the resources in your cluster.
You can enable/disable watching a resource using the following command:

1. Helm: `--set watcher.resources.RESOURCE=true/off`


### Namespaces

The Komodor agent watches all the namespaces (by default `watchNamespace=all`)

To watch a single namespace use the following command:

1. Helm: `--set watcher.watchNamespace=NAMESPACE`


#### Denylist

Using `namespacesDenylist` you can opt list of namespaces

### Agent Tasks

Agent tasks are used to interact with the cluster on demand, read more about interaction with the cluster [here](./Interaction-With-The-Cluster.md)

To enable agent tasks (default is `off`):

1. Helm: `--set watcher.enableAgentTaskExecution=true && --set watcher.allowReadingPodLogs=true`

### Environment Variables

Alternativly, you can pass the configuration as environment variables using the `KOMOKW_` prefix and by replacing all the . to _, for the root items the camelcase transforms into underscores as well.

For example:

```bash
# apiKey
KOMOKW_API_KEY=9950ef9b-e436-4f04-9885-23b9a597b3b0
# watcher.resources.replicaSet
KOMOKW_RESOURCES_REPLICASET=false

# watcher.watchNamespace
KOMOKW_WATCH_NAMESPACE=my-namespace
# watcher.collectHistory
KOMOKW_COLLECT_HISTORY=true
```

## Updating the agent
### Helm

```bash
helm repo update
helm upgrade --install k8s-watcher komodorio/k8s-watcher --reuse-values
```

## Uninstalling


### Helm

```bash
helm uninstall k8s-watcher
```
