# LaunchDarkly Integration

Integration with LaunchDarkly extends the holistic view of the environment with flags changes.
For example:
* Feature flag was turned on
* Feature flag invariation changed
* Feature flag targeting was changed

## Installation

In order to create that integration all you need is to use navigate to [LaunchDarkly Webhook Integration](https://app.launchdarkly.com/default/integrations/webhooks/new) and fill the form:
1. Name - give your integration a name
2. URL - __Please contact us to provide you the URL__ (we also will provide you a secret to sign the webhooks payload)
3. Sign Webhook - use the secret from Komodor
4. Add policy
   1. You can use `proj/*:env/*:flag/*` statement to tell LaunchDarkly to send to Komodor all the changes for all your flags across all your environments. You may use the "Resource finder" to customize it for your needs.
   2. Set the effect to "Allow"
   3. Choose all actions

![image](https://docs.launchdarkly.com/static/c8f2ec43853827df1983cbc739c774ac/d4377/integrations-webhooks-create.png)