# lib_SAML
This is the SAML 2.0 Authentication library for Convertigo platform. Install this library to enable SAML 2.0 SSO to your Convertigo applications.

# Installation

* In your Convertigo Studio use File->Import->Convertigo->Convertigo Project and hit the 'Next' button

* In the Dialog 'Project remote URL' field Paste :

        lib_SAML=https://github.com/convertigo/c8oprj-lib-saml.git

* And click the 'Finish' button

# Usage

## Configuring your SSO IDP (Identity provider)

You will need at least 2 Fields to be configured in your SSO IDP :
 * The Identifier (Entity ID) 
 * The Reply URL (Assertion Consumer Service URL)

Here is the what you have to configure in these fields :

Field | value
------| ------
Entity ID | Your Convertigo &lt;server URL&gt; for example, https://mysite.convertigo.net/convertigo for a Convertigo cloud instance
Assertion Service URL (ACS URL) | The URL to your Convertigo SAML API endpoint. This is set to your &lt;Server URL&gt;/api/SAML. for example https://mysite.convertigo.net/convertigo/api/SAML

## Flows

### Classic flow.

When a user access your application, you must redirect it to the SSO IDP. The IDP will present the user a Sign In dialog if he is not already signed with it. When the sign in is complete, the IDP will redirect the user to your application.

