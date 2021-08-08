# PagerDuty Integration

PagerDuty Integration adds __PagerDuty Incident__ events to your service events.

**NOTE: Currently we support PD events that originate on Datadog.**

## Installation

### Prerequisites

In order for us to connect your Datadog-PD incidents to your services on Komodor, we need to find a match between environment variables found on the Datadog service and your service on K8s.

Please make sure the following environment variables exist on your K8s deployment:
- `DD_ENV` should match the environment specified on the Datadog service
- `DD_SERVICE` should match the service name specified on the Datadog service

### Installation Steps

1. Make sure the prerequisites above are met.
1. Locate the PagerDuty installation tile on [Komodor Integration Settings](https://app.komodor.com/main/integration).
1. Press __Install__.
1. At this point you should be redirected to Pagerduty and back to Komodor successfully.

### Confirmation

1. A PagerDuty Integration tile will be added to the top section of labeled __Installed Integrations__.
1. When an issue from Datadog is raised through PD, you will be able to find it in the appropriate Komodor service page.