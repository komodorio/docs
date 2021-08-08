# Datadog Integration

Komodor-Datadog integration allows you to see service connections on Komodor. Services that are detected as related by Datadog will be added to the __Related Services__ section in the Komodor Service View.

## Installation

### Prerequisites

In order for us to connect your services according to Datadog tracing, the following environment variables should exist on your k8s deployments:
- `DD_ENV` should match the environment specified on the Datadog service
- `DD_SERVICE` should match the service name specified on the Datadog service

### Installation Steps

1. Make sure the prerequisites above are met.
1. Locate the Datadog installation tile on [Komodor Integration Settings](https://app.komodor.com/main/integration).
1. Press __Install__.
1. Follow instructions on the screen.

### Confirmation

1. A Datadog Integration tile will be added to the top section of labeled __Installed Integrations__.
1. Your services that interact with each other should appear under the __Related Services__ section in the Komodor service page.