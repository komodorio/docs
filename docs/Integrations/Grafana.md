# Grafana Integration

Grafana Integration adds __Grafana Alerts__ events to your service on Komodor.

## Installation

### Prerequisites

A running instance of Grafana.

### Installation Steps

1. Make sure the prerequisites above are met.
1. Locate the Grafana installation tile on [Komodor Integration Settings](https://app.komodor.com/main/integration).
1. Press __Install Integration__. A dialog will open.
1. Go to your Grafana instance.   
1. In the Grafana side bar, hover your cursor over the Alerting (bell) icon and then click `Notification channels`.
1. Press __New channel__.
1. In the `Name` field, enter a name for the channel.
1. In the `Type` field, choose _webhook_.   
1. Copy the webhook URL to the `Url` field.
1. Open the `Notifications settings`.
1. Check the __Default__ option. When selected, this option sends a notification on this channel for all alert rules.
1. Press __Save__
1. Press __Install Grafana Installation__

### Confirmation

1. A Grafana Integration tile will be added to the top section of labeled __Installed Integrations__.
1. When a Grafana alert is triggered it will be added to the relevant service on Komodor.
