# Datadog Integration

DataDog integration allows DataDog Monitor Alerts to be available in Komodor and to suggest related service based on services connection deteced by DataDog.

### Prerequisites

For Komodor service correlation, your services according to Datadog, the following DataDog's service tags should be available on the resources.
- environment - should match the environment specified on the Datadog service (`DD_ENV`)
- service - should match the service name specified on the Datadog service (`DD_SERVICE`)

DataDog's tags can be done by environment variables, labels, and annotations.
To do the correlation, the tags must be a string value and not a reference value.

For more information about DataDog tags for Kubernetes go into [DataDog tagging documentation](https://docs.datadoghq.com/getting_started/tagging/unified_service_tagging/?tab=kubernetes)
### Installation Steps

1. Make sure the above prerequisites are met.
1. Locate the Datadog installation tile on [Komodor Integrations](https://app.komodor.com/main/integration) page.
1. Press __Install Integration__.
1. Follow the on screen instructions.

### Confirmation

1. A Datadog Integration tile will be added to the top section under __Installed Integrations__.
1. Your services that interact with each other will appear under the __Related Services__ section in the Komodor services page.