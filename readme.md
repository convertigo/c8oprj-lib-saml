# lib_SAML
This is the SAML 2.0 Authentication library for Convertigo platform. Install this library to enable SAML 2.0 SSO to your Convertigo applications.

# Installation

* In your Convertigo Studio use File->Import->Convertigo->Convertigo Project and hit the 'Next' button

* In the Dialog 'Project remote URL' field Paste :

        lib_SAML=https://github.com/convertigo/c8oprj-lib-saml.git

* And click the 'Finish' button

# Usage

## Configuring your SSO IDP (Identity provider)

You will need at least 2 Fields to be configured in your SSO IDP when you will declare a new application :
 * The Identifier (Entity ID) 
 * The Reply URL (Assertion Consumer Service URL)

Here is the what you have to configure in these fields :

Field | value
------| ------
Entity ID | Your Convertigo &lt;server URL&gt; for example, this should be set to __https://&lt;mysite&gt;.convertigo.net/convertigo__ for a Convertigo cloud instance
Assertion Service URL (ACS URL) | The URL to your Convertigo SAML API endpoint. This is should be set to your &lt;Server URL&gt;/api/SAML. for example __https://&lt;mysite&gt;.convertigo.net/convertigo/api/SAML__

Find below links to Configure SSO for classic IDP providers :

Provider | Link
-------- | ------------
Google Web & Mobile Apps |  https://admin.google.com/ac/apps/unified
Microsoft Azure Active Directory |  https://portal.azure.com/#blade/Microsoft_AAD_IAM/StartboardApplicationsMenuBlade/AllApps/menuId/



## Configuring Convertigo Symbols

lib_SAML needs some symbols to be configured. You configure them trough the Web Console: https://&lt;your site&gt;.convertigo.net/admin, hit the ___symbols___ button to get to the symbol configuration page.


Symbol  | value
------| ------
lib_SAML.IdpSSOServiceURL | The IDP Service URL. This information is available once you configured a new application in the IDP. for example for Azure Directory, something like : https://login.microsoftonline.com/8a22dd7e-cfa3-4d41-8370-e59bb65a8a72/saml2 or for Google Login, something like : https://accounts.google.com/o/saml2/idp?idpid=C02myon1q
lib_SAML.lib_SAML.SPEntityID | You application's Entity ID. The same you configured in your SSO Idp. for example : __https://&lt;mysite&gt;.convertigo.net/convertigo__ 


## Flow

### SAML 2.0 Classic flow (Authentication Request Protocol).

When a user access your application, he will be redirected the SSO IDP. The IDP will present the user a Sign In dialog if he is not already signed with it. When the sign in is complete, the IDP will redirect the user to your application. To do this the SAML Token is stored in the Convertigo Sesson. 

## Shared Component

To enable SSO in your app, you just have to insert the __SAMLLogin__ shared component in the first page of your app. This will automatically trigger the _AuthnRequest_ Flow and redirect to the IDP if not already Authenticated.

Once authenticated, the global variable _SAMLNameID_ will hold the authenticated SAML attribute _NameID_. Be sure to configure your IDP provider to set a proper information for _NameID_ in the attribute mappings. 

## Sample Application

You will find in this project a sample application using the __SAMLLogin__ shared component. Be sure to configure your IDP and the Convertigo symbols accordingly to run the app.


