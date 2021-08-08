# Config Change API Integration

Config change API allows users to send changes in their config (from internal tools and infrastructure), and see them as part of the Komodor Service view.

### How to use

##### Request URL
Mandatory query params will be used for service selection:
* serviceName 
* namespace
* clusterName

##### Authentication
To authenticate the request use API Key on your "REST API" integration tile in the Komodor app and add it to a header with `X-API-KEY` name.

 
 _URL example_:
 https://api.komodor.com/v0/event/config_change?serviceName=backend-service?namespace=default&clusterName=production"


##### Body

This is the event itself with the relevant configuration you want to be connected to the service as JSON.
	`{ key1: value1, key2: value2… }`

### Full Example


`curl H "X-API-KEY: <rest api key>" -H "Content-Type: application/json" -d '{"key":"value"}' 'https://api.komodor.com/v0/event/config_change?serviceName=backend-service?namespace=default&clusterName=production"
`
