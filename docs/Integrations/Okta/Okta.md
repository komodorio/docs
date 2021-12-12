# Okta Integration

Only Okta administrators can add Komodor, if you aren't an Okta administrator, please contact him.

Here are the steps in order to integrate Komodor with Okta:

1. Go to Okta admin -> Applications -> Browse App Catalog

   ![BrowseAppCatalog](./browse_app_catalog.png)

2. Search fot Komodor and click 'Add'

   ![SearchKomodor](./search_komodor.png)

   ![AddKomodor](./add_komodor.png)

3. In the 'Application Label' you can enter what you want. It is for internal use and will be your nickname for the App.
   ![OktaApplicationLabel](./okta_application_label.png)

4. Go to application -> 'Sign On' tab -> 'Settings' and click 'Edit'

5. In 'Advanced Sign-on settings' enter variable of 'Account Name' and pass this varibale to us (in example: 'Komodorio').
   ![KomodorioAccountName](./komodorio_account_name.png)

6. Click 'View Setup Instructions' and then pass the 'Metadata URL' to us (with the Account Name variable)
