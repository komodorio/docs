# Sentry Integration

The Sentry integration allows you to see sentry issues in Komodor. For each service, Komodor automatically maps the relevant Sentry project to Komodor services and allows you to gain a full-service timeline: both relevant changes (deploys, config changes etc’) and issues from Sentry will all be in one place.

## Installation


### Installation Steps

1. Make sure the services you track in Komodor use the SENTRY_DSN environment variable.
1. Locate the Sentry installation tile on the [Komodor Integrations](https://app.komodor.com/main/integration) page.
1. Click __Install Integration__.
1. A dialog will open with a webhook URL and a link to Sentry to define an internal integration.
1. Go to your Sentry account and click on settings in the left menu. Click on Developer Settings in the settings menu:
![image6](https://user-images.githubusercontent.com/13674505/106886073-21c7f680-66ec-11eb-9129-91b36a84223c.png)
1. Click on + New Internal Integration
![image3](https://user-images.githubusercontent.com/13674505/106886157-3dcb9800-66ec-11eb-9597-82e087b9a7ea.png)
1. Name this integration Komodor.
1. Paste the webhook URL in the webhook field:
![image2](https://user-images.githubusercontent.com/13674505/106886329-6d7aa000-66ec-11eb-930a-c1095ae164ad.png)
1. To operate properly Komodor needs these permissions:
   1. __Project__ - Read
   1. __Issue & Event__ - Read
![image1](https://user-images.githubusercontent.com/13674505/106886407-87b47e00-66ec-11eb-835b-07e743b0fc3d.png)
1. Check the `issue` webhook checkbox
![image7](https://user-images.githubusercontent.com/13674505/106886489-9e5ad500-66ec-11eb-9112-924a5c8b8e05.png)
1. Save changes
1. As soon as you save you will see your “client secret”. Copy the value:
![image4](https://user-images.githubusercontent.com/13674505/106886584-b7fc1c80-66ec-11eb-9f15-c4e09139c086.png)
1. Go back to your Komodor integrations page and paste the value of your client secret to the client secret text box.
1. Click
`Install`

### In your deployment.yaml

We use the value of the environment variable `SENTRY_DSN` to match __Sentry Issue__ events with your services in Komodor.

Make sure your kubernetes deployment has the environment variable `SENTRY_DSN`.

### Confirmation

1. A Sentry Integration tile will be added to the top section under __Installed Integrations__.
1. Once completed you will be able to see Sentry events in you services view:
![image5](https://user-images.githubusercontent.com/13674505/106886842-0ad5d400-66ed-11eb-9352-2cabb12975a8.png)

