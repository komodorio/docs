# Opsgenie Alert Event Integration

Opsgenie integration allows Opsgenie Alerts to be available in Komodor timelines.

---

## Installation

### The Opsgenie integration involves 3 steps:

1. Enabling the integration in Komodor.
2. Integrate Opsgenie with Webhook.
3. Adding labels to the alert.

---

### 1. Enabling the integration in Komodor

To enable the Komodor Opsgenie integration go to [Komodor integrations page](https://app.komodor.com/main/integration), select Opsgenie and install the integration.

### 2. Integrate Opsgenie with Webhook

Follow the following documentation to create an Opsgenie [webhook](https://support.atlassian.com/opsgenie/docs/integrate-opsgenie-with-webhook/). 
![add_integration](./img/Opsgenie/add_integration.png)

### 3. Adding labels to the alert.

By default, an Opsgenie alert will be added to the Komodor timeline as a "Cross-service event".
To associate Opsgenie alerts to specific/multiple workloads, it is required to specify the labels associated with the relevant Kubernetes workloads as [extra properties](https://support.atlassian.com/opsgenie/docs/alert-fields/) of the Opsgenie alert.

```yaml
<label_name>: <label_value>
```
