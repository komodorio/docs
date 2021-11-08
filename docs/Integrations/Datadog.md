# Datadog Integration

Komodor-Datadog integration allows you to see service connections in Komodor. Services that are detected as related by Datadog will be added to the __Related Services__ section in the Komodor Services View.

## Installation

### Prerequisites

In order for us to connect your services according to Datadog tracing, the following environment variables should exist on your kubernetes deployments:
- `DD_ENV` should match the environment specified on the Datadog service
- `DD_SERVICE` should match the service name specified on the Datadog service

### Installation Steps

1. Make sure the above prerequisites are met.
1. Locate the Datadog installation tile on [Komodor Integrations](https://app.komodor.com/main/integration) page.
1. Press __Install Integration__.
1. Follow the on screen instructions.

### Confirmation

1. A Datadog Integration tile will be added to the top section under __Installed Integrations__.
1. Your services that interact with each other will appear under the __Related Services__ section in the Komodor services page.