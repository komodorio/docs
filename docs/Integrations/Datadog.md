# Datadog Integration


DataDog integration allows DataDog Monitor Alerts to be available in Komodor and to suggest related service based on services connection deteced by DataDog.

- [DataDog's Komodor Integration Page](https://app.datadoghq.com/integrations/komodor?search=komo)
- [Komodor's DataDog  Integration Page](https://app.komodor.com/main/integration)


## Install the Komodor platform integration
 This first integration step allows Komodor to access your Datadog account via API key and Token key, and to **suggest related services based on service dependencies** detected in Datadog.

## Install the Datadog Webhook integration
 This allows Komodor to receive alerts from Datadog monitors. You can see all alerts in the Komodor Service View.

## Configure a Datadog monitor notification
Adding a Komodor dynamic link to Datadog monitor notifications generates a direct link to the relevant service in Komodor. See the alert link in your Alerting provider connected to Datadog.

## Configure Hyperlinks 

## Configure Taggiing  


Use Kubernetes annotations to enrich the Komodor service and deployment screens with links to relevant Datadog APM dashboards, as well as dynamic links to specific service metrics and time ranges within Datadog.

## Uninstallation
This will remove the Integration’s functionality and included assets from your organization.



## Instructions

## Create the DataDog Integration in the Komodor

Follow the link to the [Komodor Integrations page](https://app.komodor.com/main/integration).  

Find this Icon ![Create Integration with DataDog](https://raw.githubusercontent.com/komodorio/docs/datadog-markdown-update/docs/img/DataDog-CreateIntegration.png) 

Press the button Install Integration button

---

Once you have created the Integration it will look like this. Make a copy of license. This key will be used in the next step.
![Created Integration with Liocense key](https://raw.githubusercontent.com/komodorio/docs/datadog-markdown-update/docs/img/DataDog-IntegrationCreated.png)

Grab a copy of the license key. The key will be used in the next step


## Create Webhook in Komodor 

Next proceed to the [DataDog Webhook integration](https://app.datadoghq.com/integrations/webhooks?search=webhook) 

Create a new Webhook.  The [payload is json](https://github.com/komodorio/docs/blob/datadog-markdown-update/docs/img/webhook-payload.json) template.  Copy the JSON payload into the DataDog Webhook configuration


Add an HTTP Header.  We use the licesne key from the previous step.  
```
{"X-API-KEY":"XXXXXXXX-aaaaaaaaaa-xxxxxx-7510"}
```
Copy the license to bottom of the webhook configuration page. 

It will look like this
![DataDog Create Webhook](https://raw.githubusercontent.com/komodorio/docs/datadog-markdown-update/docs/img/DataDog-Webhook-Edit.png)



## Deployment Manifest Configuration / DataDog Service Tags


For Komodor service correlation, your services according to Datadog, the following DataDog's service tags should be available on the resources.

- environment - should match the environment specified on the Datadog service (`DD_ENV`)
- service - should match the service name specified on the Datadog service (`DD_SERVICE`)

DataDog's tags can be enabled by environment variables, labels, and annotations.
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
2. 
