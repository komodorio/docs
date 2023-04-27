# Configure JumpCloud SSO
- This tutorial is based on [this article][1] from JumpCloud.
- Access the JumpCloud Administrator Console at https://console.jumpcloud.com.
- Go to **USER AUTHENTICATION > SSO**.
- Click **( + Add New Application )** to configure a new application.
- Search for **Auth0**, then click **configure**.
- Enter a Display Label in the General Info tab. **Komodor** is recommended.
### Configure SAML
- Go to the SSO tab
    - choose a TEAMNAME, preferably your company name, and replace it in the following steps
    - Change the **IDP URL** suffix to `komodor`
    - Change the **IdP Entity ID** to `https://komodorio.com`
    - Change the **SP Entity ID** to `urn:auth0:komdoorio:TEAMNAME`
    - Change the **ACS URL** to `https://auth.komodor.com/login/callback?connection=TEAMNAME`
- Click **activate**.
- Click **continue** on the confirmation window.
- Click **Download Certificate** in the top right of the window.
  - Alternatively, you can copy the Metadata URL and send this info.
### Contact Komodor
- Update your komodor contact with the following information:
    - The TEAMNAME
    - Send the certificate file / metadata URL

## Next steps
- Now  you'll need to authorize user access to Komodor.
    - see [here][2] for more info.
- Wait for an approval from your komodor contact that the connection is ready to test.

- The tutorial is now complete. You can now login to Komodor using your JumpCloud credentials.

[1]: https://support.jumpcloud.com/support/s/article/single-sign-on-sso-with-auth0#configure-jumpcloud-2
[2]: https://support.jumpcloud.com/support/s/article/authorize-users-to-an-sso-application-2019-08-21-10-36-47
