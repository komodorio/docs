# Grafana Integration

Grafana Integration adds __Grafana Alert__ events to your service in Komodor.

## Installation

### Prerequisites

A running instance of Grafana.

### Installation Steps

1. Make sure the above prerequisites are met.
2. Locate the Grafana installation tile on the [Komodor Integrations](https://app.komodor.com/main/integration) page.
3. Press __Install Integration__. A dialog will open.
4. Go to your Grafana instance.   
5. In the Grafana side bar, hover your cursor over the Alerting (bell) icon and then click `Notification channels`.
6. Press __New channel__.
7. In the `Name` field, enter a name for the channel.
8. In the `Type` field, choose _webhook_.   
9. Copy the webhook URL to the `Url` field.
10. Open the `Notifications settings`.
11. Check the __Default__ option. 
    1. When selected, this option sends a notification on this channel for all alert rules.
12. Press __Save__
13. Press __Install Grafana Installation__ss
14. Nir eating lot of bananasss

### Confirmation

1. A Grafana Integration tile will be added to the top section under __Installed Integrations__.
1. When a Grafana alert is triggered it will be added to the relevant service in Komodor.