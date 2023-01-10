# Webhook Notification

Komodor supports notifications using a custom webhook.

##  Prerequisites
- Webhooks via HTTPS only   
- Desired destination URL  


## Define Webhook Notification
1. On the “Monitors” page, choose your desired cluster and specific monitor  
2. On the “Edit Role” section, select “Webhook” as notification definition  
If you have already set up a notification channel - choose one from the list, if not, create the wanted channel with the following configuration:
    1. **Webhook URL** - The destination URL to which notifications will be sent
    2. **Webhook Name** - Choose a meaningful name
3. Save Monitor  

After completing the monitor configuration, you can use the created channel on any other monitor

Webhook notifications will be sent as a POST in JSON format to your webhook endpoint. 

The webhook feature will allow you to integrate into the following channels:  

1. Prometheus Alert Manager  
2. ServiceNow notification

## Example of POST data

Monitor types: availability, node, PVC, job, cronJob  
Status: open / close  
Close time will appear only when the “close” message is sent”   

    {   
    	"cluster": " production",
	    "namespace": "default",
	    "serviceName": "komodor.production-default.brain-consumer-pg",
	    "resourceName": "brain-consumer-pg",
	    "status": "open",
	    "startTime": "0001-01-01 00:00:00 +0000 UTC",
	    "closeTime": "<no value>",
	    "monitorType": "availability",
	    "issueURL": "https://app.komodor.com/main/deep-dive/komodor.production-default.brain-consumer-pg?timeWindow=-62135596805000-1672945087683&timeframe=custom&eventId=1486f269-e28e-4498-8389-9ca33c1f647a",
	    "issueDetails": "[Terminating ContainersNotReady]"
    }

