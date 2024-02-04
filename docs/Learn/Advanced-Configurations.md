
# Advanced Agent Configuration Guide

To tailor the agent's functionality, modify the [helm values file](https://github.com/komodorio/helm-charts/blob/master/charts/komodor-agent/values.yaml). For a comprehensive overview of configurable parameters, refer to the detailed list [here](https://github.com/komodorio/helm-charts/blob/master/charts/komodor-agent/README.md#values).

To set up or update the agent, use the following commands:

```bash
helm repo add komodorio https://helm-charts.komodor.io
helm repo update
helm upgrade --install komodor-agent komodorio/komodor-agent \
  --set apiKey=<YOUR_API_KEY_HERE> \
  --set clusterName=<CLUSTER_NAME> \
  -f <PATH_FOR_VALUES_FILE>
```

It's advisable to maintain the values file for each cluster in source control, which can then be referenced during agent upgrades:

```bash
helm upgrade --install komodor-agent komodorio/komodor-agent \
  -f <path_to_values_file>
```

---
## Modifying Resource Requests and Limits for Agent Components
Agent components are initially set up with standard requests and limits tailored for enterprise customers. However, these settings can be customized by modifying specific values in the values file. The following agent components allow such configuration:

* `komodorAgent.watcher.resources`
* `komodorAgent.supervisor.resources`
* `komodorAgent.networkMapper.resources`
* `komodorAgent.metrics.resources`
* `komodorDaemon.metrics.resources`
* `komodorDaemon.metricsInit.resources`
* `komodorDaemon.networkSniffer.resources`
* `komodorDaemon.nodeEnricher.resources`

For instance, to adjust the resource requests and limits for the watcher container in the komodor-agent deployment, use the following YAML configuration:

```yaml
components:
  komodorAgent:
    watcher:
      resources:
        requests:
          cpu: 100m
          memory: 128Mi
        limits:
          cpu: 200m
          memory: 256Mi
```

---
## Updating Image Repository Configuration

The chart is set up to use `public.ecr.aws/komodor-public` as the default image repository.

If you need to use an alternative repository, such as a private one, you can change the `imageRepo` value in the values file. For example, to switch to the `myrepo/komodor-agent` repository, apply the following YAML configuration:

```yaml
imageRepo: myrepo/komodor-agent
```
---

## Disabling a specific capability
By default, most capabilities are enabled. To disable a specific capability, set the relevant value to `false` in the values file.
the following capabilities can be disabled:

* `metrics`
* `networkMapper`
* `actions`
* `helm`
* `nodeEnricher`

For example, to disable the `metrics` capability, apply the following YAML configuration: <br />

```yaml
capabilities:
  metrics: false
```
---

## Limiting the agent to watch specific namespaces
By default, the agent watches all namespaces. To limit the agent to watch a specific namespace, set the `events.watchNamespace` value in the values file.

For example, to limit the agent to watch the `default` namespace, apply the following YAML configuration:

```yaml
events:
  watchNamespace: default
```

You can also specify a list of namespaces to avoid watching by settings the `events.namespaceDenyList` value in the values file.

For example, to avoid watching the `kube-system` and `kube-public` namespaces, apply the following YAML configuration:

```yaml
events:
  namespaceDenyList: ["kube-system", "kube-public"]
```
---

## Data redaction configuration
In some cases, you may want to redact sensitive data from the komodor platform. You can do so by the following values:

* `events.redact` - Redact values from specific fields in resources
* `logs.redact` - Redact values from logs
* `logs.NamespaceDenylist` - Do not collect logs from specific namespaces
* `logs.NamespaceAllowlist` - Only collect logs from specific namespaces
* `logs.NameDenylist` - Do not collect logs from specific workloads

For example, to redact the `password` field from all resources, apply the following YAML configuration:

```yaml
events:
  redact:
    - "PG_.*"
    - ".*PASSWORD.*"
```

To avoid collecting logs from the `kube-system` namespace, apply the following YAML configuration:

```yaml
logs:
  namespaceDenylist: ["kube-system"]
```

To allow only collecting logs from the `default` and `dev` namespaces, apply the following YAML configuration:

```yaml
logs:
  namespaceAllowlist: ["default", "dev"]
```

To mask passwords in logs, apply the following YAML configuration:

```yaml
logs:
  redact:
    - "password=(.+?)\b"
    - "(?U)\"sessionId\": (\".+\"{1})"
```

example logs redactions:
```json
INPUT: example my password=supersecret and something else
OUTPUT: example my <REDACTED> and something else

INPUT: { "level": "INFO", "message": "User has added Item 12453 to Basket", "sessionId": "SESS456", "timestamp": 1634477804 }
OUTPUT: { "level": "INFO", "message": "User has added Item 12453 to Basket", <REDACTED>, "timestamp": 1634477804 }
```

---

## Setting Annotations, and Selectors for Deployed Workloads

The `komodor-agent` deployment and `komodor-agent-daemon`  can be customized with specific Kubernetes fields to enhance workload management. You can configure these fields by setting the following values:

* `components.<component>.annotations` - Add custom annotations to the workload.
* `components.<component>.affinity` - Define affinity rules for the workload.
* `components.<component>.nodeSelector` - Specify node selectors for the workload.
* `components.<component>.tolerations` - Set tolerations for the workload.
* `components.<component>.podAnnotations` - Add annotations directly to the pods in the workload.

To illustrate, if you want to add the annotation `app.kubernetes.io/name: komodor-agent` to the komodor-agent deployment, you would use this YAML configuration:

```yaml
components:
  komodorAgent:
    annotations:
      - app.kubernetes.io/name: komodor-agent
```
---

## Communicate using a proxy server
If you need to communicate with the Komodor platform using a proxy server, you can set the following values in the values file:

* `proxy.enabled` - Set to `true` to enable proxy communication.
* `proxy.httpProxy` - Set the HTTP proxy address.
* `proxy.httpsProxy` - Set the HTTPS proxy address.
* `proxy.noProxy` - Set specific domains to ignore proxy for.

For example, to enable proxy communication and set the proxy address to `http://myproxy:8080`, apply the following YAML configuration:

```yaml
proxy:
  enabled: true
  httpProxy: http://myproxy:8080
```

---

## Configure the agent with a custom CA certificate
If you need to configure the agent with a custom CA certificate, you can set the following values in the values file:

* `customCa.enabled` - Set to `true` to enable custom CA certificate configuration.
* `customCa.secretName` - Set the name of the secret containing the CA certificate.

For example, to enable custom CA certificate configuration and set the secret name to `my-secret`, apply the following YAML configuration:

```yaml
customCa:
  enabled: true
  secretName: my-secret
```
where the secret contains the CA certificate in the `ca.crt` key.