# Datadog Webhook Integration

Komodor-Datadog webhook integration allows Komodor to receive alerts from Datadog Monitors. You will see all alerts in the Komodor Service View.

## Installation

### Prerequisites

In order for us to connect your services according to Datadog events, the following environment variables should exist on your k8s deployments:
- `DD_ENV` should match the environment specified on the Datadog tags
- `DD_SERVICE` should match the service name specified on the Datadog tags

### Installation Steps

1. Make sure the prerequisites above are met.
1. Locate the Datadog installation tile on [Komodor Integration Settings](https://app.komodor.com/main/integration).
1. Press __Install__.
1. Follow instructions on the screen.

### Confirmation

1. A Datadog Integration tile will be added to the top section of labeled __Installed Integrations__.

### Configuring the webhook in Datadog

1. Go to [Datadog Webhook Integration Setup](https://app.datadoghq.com/account/settings#integrations/webhooks)
1. Create a `+ New` Webhook
1. Call the webhook `komodor`
1. Enter the webhook server URL in the URL field: https://app.komodor.com/collector/datadog/webhook
1. Copy the following Payload schema into the Payload field:
```json
    {
    "body": "$EVENT_MSG",
    "last_updated": "$LAST_UPDATED",
    "event_type": "$EVENT_TYPE",
    "title": "$EVENT_TITLE",
    "date": "$DATE",
    "org": {
        "id": "$ORG_ID",
        "name": "$ORG_NAME"
    },
    "id": "$ID",
    "tags": "$TAGS",
    "alert": {
        "id": "$ALERT_ID",
        "type": "$ALERT_TYPE",
        "transition": "$ALERT_TRANSITION",
        "cycleId": "$ALERT_CYCLE_KEY",
        "priority": "$PRIORITY",
        "status": "$ALERT_STATUS",
        "scope": "$ALERT_SCOPE",
        "query": "$ALERT_QUERY",
        "metric": "$ALERT_METRIC",
        "metric_namespace": "$METRIC_NAMESPACE"
    },
    "aggregation_key": "$AGGREG_KEY",
    "link": "$LINK",
    "snapshot": "$SNAPSHOT",
    "user": "$USER",
    "username": "$USERNAME",
    "email": "$EMAIL"
}
```

1. Add a Custom Header `X-API-KEY` with the Api Key found in the Komodor Integration page from the Datadog integration tile at the bottom of the setup modal in a JSON format.

```bash
    {"X-API-KEY": "YOUR_KOMODOR_API_KEY"}
```

1. Save your changes
1. For every monitor you wish to receive alerts to Komodor. Edit the monitor and add `@webhook-komodor` at the end of the Monitor message.
