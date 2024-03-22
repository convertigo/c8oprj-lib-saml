


# lib_SAML

#This is the Back end part of the Convertigo SAMLv2 Connector

The Connector works with the front-end part available here :  https://github.com/convertigo/c8oprj-lib-saml-ui-ngx

## Symbols

|Name           				| Usage 
----------------------------|------
|lib_SAML.cert				| The certificate use to sign AuthnReqests in .cer format (Copy / paste the content of your .cer file to the value of the symbol) |
|lib_SAML.key.secret 		| The private key used to sign AuthN request associate with the certificate in .key format (Copy / paste the content of your .key ||file to the value of the symbol) |
|lib_SAML.IdpSSOServiceURL  | The Idp's Service URL  |
|lib_SAML.SPEntityID  		| The Service ID configured in the SAML IDP. |





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

##### Operations

###### PostOperation

**Parameters**

<table>
<tr>
<th>name</th><th>comment</th>
</tr>
<tr>
<td>RelayState</td><td></td>
</tr>
<tr>
<td>SAMLResponse</td><td></td>
</tr>
</table>



