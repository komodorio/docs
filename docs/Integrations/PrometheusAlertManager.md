# Prometheus Alert Manager Integration

Integration with alert manager reports alerts also to Komodor. We connect the alert to the Kubernetes workload and display the events on the timeline.

## Installation

### The Alert Manager integration involves 2 parts:

1. Enabling the integration in Komodor.
2. Creating webhook on the alert manager and adding labels to the alert.

### Enabling the integration in Komodor

To enable the Komodor Prometheus Alert Manager integration go to [Komodor integrations page](https://app.komodor.com/main/integration) and select Prometheus Alert Manager.

### Creating webhook and configure labels

1. Open your `alertmanager.yml` configuration file
2. Add receiver to your receivers name `komodor` and his sink is `webhook_configs` as the URL from the integration, while set resolved is set to `true`.

```yaml
receivers:
  - name: komodor
    webhook_configs:
      - url: "<URL_FROM_KOMODOR>"
        send_resolved: true
```

3. Then also in `alertmanager.yml` configure the route so alert will come to komodor

```yaml
route:
  receiver: komodor
```

If you already have receivers you can config many of them like that:

```yaml
routes:
  - match:
      severity: critical
    receiver: pagerduty
  - match:
    receiver: komodor
```

Please note about the [routing rules](https://prometheus.io/docs/alerting/latest/configuration/#route) of Alert Manager. Note that if `continue` is set to false, it stops after the first matching child. If `continue` (continue default is false).

Full yaml can look like that:

```yaml
global:
  group_interval: 5m
  repeat_interval: 12h
routes:
  - match:
    receiver: komodor
receivers:
  - name: komodor
    webhook_configs:
      - url: "<URL_FROM_KOMODOR>"
        send_resolved: true
```

4. Please note to specify 2 **labels** on the alert in order to connect them to the Kubernetes workload:

```yaml
service: <workload-name>
cluster: <cluster-name>
```

5. [Optional] defining custom description to the alert on Komodor (specify it in the **annotation**):

```yaml
description: <content>
```
