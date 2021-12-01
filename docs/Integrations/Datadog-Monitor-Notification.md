# Datadog Monitor Notification

Adding A Komodor dynamic link to DataDog Monitor Notifications will generate a direct link to the relevant service in Komodor.
You will see the alert link in your Alerting provider connected to DataDog.

## Installation

### Prerequisites

To use DataDog variables in monitor notifications, there are two prerequisites imposed by DataDog:
1. Make sure there are variables defined for: cluster name, namespace, service name.
2. Make sure the tags are used in the monitor, or grouped by them.

### Link Setup

1. Make sure the prerequisites above are met.
2. Add the dynamic link to the DataDog monitor notification message: *
`https://app.komodor.com/main/deep-dive/YourAccountName.{{cluster_name}}-{{namespace}}.{{service_name}}`

* Please note variable names will vary depending on your local DataDog setup.

Example:

For account `greatcompany` alerting PagerDuty.

variables: cluster_name `k8s_clustername` ,namespace `k8s_namespace`, service_name `k8s_servicename`
The dynamic link will be:

```bash
@pagerduty-Datadog 
https://app.komodor.com/main/deep-dive/greatcompany.{{k8s_clustername}}-{{k8s_namespace}}.{{k8s_servicename}}
```

### Confirmation and testing

1. Dynamic Komodor link will be added to your next DataDog alert.
2. The link will include the relevant information.

#### Testing

1. For an end-to-end testing, add the dynamic link to a test monitor and use the 'Test Notification' button in DataDog.  
2. Use the generated link in your alert provider and make sure it directs you to the correct service in Komodor.
3. If the link fails, check the [dynamic link prerequisites](https://docs.komodor.com/Integrations/Datadog-Monitor-Notification.html##prerequisites).

### See also

DataDog documentation on [monitor notifications ](https://docs.datadoghq.com/monitors/notify/#message)
