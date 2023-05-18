# PagerDuty Integration

PagerDuty Integration adds __PagerDuty Incident__ events to your services events.

**NOTE: We currently only support PD events that originate in Datadog.**

## Installation

### Prerequisites

In order to connect your Datadog-PD incidents to your services in Komodor, you need to match environment variables found in Datadog to your services in Kubernetes.

Please make sure the following environment variables exist in your kubernetes deployment:
- `DD_ENV` should match the environment specified on the Datadog service
- `DD_SERVICE` should match the service name specified on the Datadog service

### Installation Steps

1. Make sure the prerequisites above are met.
1. Locate the PagerDuty installation tile on [Komodor Integrations](https://app.komodor.com/main/integration) page.
1. Press __Install Integration__.
1. You will be redirected to Pagerduty and back to Komodor successfully.

### Confirmation

1. A PagerDuty Integration tile will be added to the top section of labeled __Installed Integrations__.
1. When an issue from Datadog is raised through PD, you will be able to find it in the appropriate Komodor services page.

### Support 
In case you encounter any issue, please contact us at support@komodor.com
