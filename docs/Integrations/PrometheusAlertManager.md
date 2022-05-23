# Prometheus Alert Manager Integration

Integration with alert manager reports alerts also to Komodor. We connect the alert to the Kubernetes workload and display the events on the timeline.

## Installation

### The Alert Manager integration involves 2 parts:

1. Enabling the integration in Komodor.
2. Creating webhook on the alert manager and adding labels to the alert.

### Enabling the integration in Komodor

To enable the Komodor Prometheus Alert Manager integration go to [Komodor integrations page](https://app.komodor.com/main/integration) and select Prometheus Alert Manager.

### Creating webhook and configure labels

1. The configuration of webhook is presented in Komodor integrations page.
2. Please note to specify 2 **labels** on the alert in order to connect them to the Kubernetes workload:

```yaml
service: <workload-name>
cluster: <cluster-name>
```

3. [Optional] defining custom description to the alert on Komodor (specify it in the **annotation**):

```yaml
description: <content>
```
