# Azure AD SSO (SAML)

> For the following part you need to contact Komodor support to receive the parameters Identifier and Reply URL (we specify below where they are needed).

Start by getting to the Azure Active Directory dashboard in the Azure portal.
From there, we navigate to "Enterprise applications":
<img src="./img/enterprise-applications.png">

Next, we click on "New application":
<img src="./img/new-application.png">

Then, click on "Create your own application":
<img src="./img/create-own-application.png">

Fill-in the application creation form as depicted below, and click "Create":
<img src="./img/app-creation-form.png">

This should lead you to the following page, where we set up the SSO connection:
<img src="./img/set-up-sso.png">

Pick SAML as your preferred SSO method:
<img src="./img/saml-connection.png">

This should lead you to the following page, where you click "Edit" on "Basic SAML Configuration":
<img src="./img/saml-based-sign-on.png">

This is where those parameters that are supplied by Komodor support (above) are required. We fill in the form as follows, and click "Save":
<img src="./img/basic-saml-configuration.png">

Next, we scroll down to the "SAML Certificates" section. We download the certificate file by clicking on the highlighted link.
Then, we copy the "Login URL" under the "Set up Komodor" section:
<img src="./img/saml-certificates.png">

Both of those need to be sent to Komodor support to finish the setup for the SAML connection to Komodor.

Once the setup is done on both sides, you can click the "Test" button to test that the sign-in works.
<img src="./img/test-sign-in.png">
