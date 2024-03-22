


# lib_SAML

This is the Back end part of the Convertigo SAMLv2 Connector. The Connector works with the front-end part available here :  https://github.com/convertigo/c8oprj-lib-saml-ui-ngx

## Symbols 

|Name           				|  Mandatory |Usage 
----------------------------|------------|---------
|lib_SAML.cert				| No | The certificate use to sign AuthN Request in .cer format (Copy / paste the content of your .cer file to the value of the symbol) |
|lib_SAML.key.secret 		| No | The private key used to sign AuthN request associate with the certificate in .key format (Copy / paste the content of your .key ||file to the value of the symbol) |
|lib_SAML.IdpSSOServiceURL  | Yes | The Idp's Service URL  |
|lib_SAML.SPEntityID  		| Yes | The Service ID configured in the SAML IDP. |

## Configuring

Basic usage need to configure only 2 symbols, the **lib_SAML.IdpSSOServiceURL** and the **lib_SAML.SPEntityID**


## Signing AuthnRequest

If you need to Sign your SAML AuthnRequest , you will have to provide a certificate with a private key in defined symbols. To generate your certificate and private key you can use openssl commands :

```
openssl genrsa  -out certificate.key 2048   
openssl req     -key certificate.key -new -x509 -days 3000 -out certificate.crt
```
This will ask you some questions :


```
Country Name (2 letter code) [AU]:
State or Province Name (full name) [Some-State]:
Locality Name (eg, city) []:
Organization Name (eg, company) [Internet Widgits Pty Ltd]:
Organizational Unit Name (eg, section) []:
Common Name (e.g. server FQDN or YOUR name) []:
Email Address []:
```
 
Be sure to enter for 'Common name' the same entity ID you configured in your IDP's SAML configuration

This will create for you certificate.key and a certificate.cer files. You can open these file with a text editor and copy/paste contents to the **lib_SAML.cert** symbol value (For the content of certificate.cer) & the **lib_SAML.key.secret** symbol value (for the content of the certificate.key)

Not configuring the **lib_SAML.cert** and **lib_SAML.key.secret** symbols will result in issuing unsigned AuthnRequests



For more technical informations : [documentation](./project.md)

- [Installation](#installation)
- [Rest Web Service](#rest-web-service)
    - [Mappings](#mappings)
        - [/SAML](#saml)
            - [Operations](#operations)
                - [PostOperation](#postoperation)


## Installation

1. In your Convertigo Studio click on ![](https://github.com/convertigo/convertigo/blob/develop/eclipse-plugin-studio/icons/studio/project_import.gif?raw=true "Import a project in treeview") to import a project in the treeview
2. In the import wizard

   ![](https://github.com/convertigo/convertigo/blob/develop/eclipse-plugin-studio/tomcat/webapps/convertigo/templates/ftl/project_import_wzd.png?raw=true "Import Project")
   
   paste the text below into the `Project remote URL` field:
   <table>
     <tr><td>Usage</td><td>Click the copy button at the end of the line</td></tr>
     <tr><td>To contribute</td><td>

     ```
     lib_SAML=https://github.com/convertigo/c8oprj-lib-saml.git:branch=8.0.0
     ```
     </td></tr>
     <tr><td>To simply use</td><td>

     ```
     lib_SAML=https://github.com/convertigo/c8oprj-lib-saml/archive/8.0.0.zip
     ```
     </td></tr>
    </table>
3. Click the `Finish` button. This will automatically import the __lib_SAML__ project


## Rest Web Service

### Mappings

#### /SAML

The POST SAML Endpoint

##### Operations

###### PostOperation

**Parameters**

<table>
<tr>
<th>name</th><th>comment</th>
</tr>
<tr>
<td>RelayState</td><td>The SAML relaystate Value</td>
</tr>
<tr>
<td>SAMLResponse</td><td>The SAML Token</td>
</tr>
</table>



