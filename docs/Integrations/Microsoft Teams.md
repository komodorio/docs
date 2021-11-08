# Microsoft Teams Integration

The Teams integration allows configuration of notifications for events such as Deploy or Health from Komodor to a Teams channel. Komodor supports different granularity levels, Cluster, Namespace and Service for each notification. The notification type, destination, and granularity can be defined in the Komodor Notifications screen.

##  Configuring Teams Notifications

###  Configuration Steps

1. Open up the Komodor [Notifications Panel](https://app.komodor.com/main/notifications/configuration). In this screen you can see all existing notifications and configure new ones.
2. Scroll to the bottom of the page and decide which type of notification you would like to create, Deployment or Health Change.

<p align="center">
  <img src="https://user-images.githubusercontent.com/28837372/140755810-57065b49-739e-4c8c-80b0-2da332364aa9.png" />
</p>

3. Select **Add this notification** for the type of notification you would like to configure.
4. Chose the cluster that you would like to alert on, or leave empty to alert on all clusters. Click **Continue** to proceed to the webhook configuration.

<p align="center">
  <img src="https://user-images.githubusercontent.com/28837372/140756824-9a6e42cb-db05-40a2-83c3-dcd2b5aa7aa8.png" />
</p>

5. Enter the channel name that you would like to post to (starting with @. "@channel" for example)
6. Retrieve the webhook URL from Teams using the on screen instructions:
	1.  Navigate to the channel where you want to add the webhook and select (•••) More Options from the top navigation bar.
	2. Choose  **Connectors**  from the drop-down menu and search for Incoming Webhook.
	3.  Select the  **Configure**  button, provide a name, and, optionally, upload an image avatar for your webhook.
	4.  The dialog window will present a unique URL that will map to the channel. Make sure that you copy and paste the URL into the "webhook URL" field.

<p align="center">
  <img src="https://user-images.githubusercontent.com/28837372/140756915-4686f3c3-defd-4e43-bcb8-246bf63f23b5.png" />
</p>

7. Click on **Create Notification** to complete the Notification Configuration

More information on Microsoft Teams integation with Webhooks can we found in the [Official Documentation](https://docs.microsoft.com/en-us/microsoftteams/platform/webhooks-and-connectors/how-to/add-incoming-webhook)
