
# ![](https://github.com/convertigo/convertigo/blob/develop/engine/src/com/twinsoft/convertigo/beans/core/images/project_color_16x16.png?raw=true "Project") lib_SAML

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
openssl genrsa  -out vertificate.key 2048   
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


<details><summary><span style="color:DarkGoldenRod"><i>Connectors</i></span></summary><blockquote><p>


## ![](https://github.com/convertigo/convertigo/blob/develop/engine/src/com/twinsoft/convertigo/beans/connectors/images/sqlconnector_color_16x16.png?raw=true "SqlConnector") void

void connector, replace or don't use it

<details><summary><span style="color:DarkGoldenRod"><i>Transactions</i></span></summary><blockquote><p>


### ![](https://github.com/convertigo/convertigo/blob/develop/engine/src/com/twinsoft/convertigo/beans/transactions/images/sqltransaction_color_16x16.png?raw=true "SqlTransaction") void

does nothing
</p></blockquote></details>
</p></blockquote></details>

<details><summary><span style="color:DarkGoldenRod"><i>Sequences</i></span></summary><blockquote><p>


<details><summary><b>Authentiticate</b> : This sequence is called by th IDP with a SAMLResponse Token</summary><blockquote><p>


## ![](https://github.com/convertigo/convertigo/blob/develop/engine/src/com/twinsoft/convertigo/beans/sequences/images/genericsequence_color_16x16.png?raw=true "GenericSequence") Authentiticate

This sequence is called by th IDP with a SAMLResponse Token. 

<span style="color:DarkGoldenRod">Variables</span>

<table>
<tr>
<th>
name
</th>
<th>
comment
</th>
</tr>
<tr>
<td>
<img src="https://github.com/convertigo/convertigo/blob/develop/engine/src/com/twinsoft/convertigo/beans/variables/images/variable_color_16x16.png?raw=true "  alt="RequestableVariable" >&nbsp;RelayState
</td>
<td>
An opaque value relayed by the IDP. In our case, the App's URL to be redirected when Auth is done
</td>
</tr>
<tr>
<td>
<img src="https://github.com/convertigo/convertigo/blob/develop/engine/src/com/twinsoft/convertigo/beans/variables/images/variable_color_16x16.png?raw=true "  alt="RequestableVariable" >&nbsp;SAMLResponse
</td>
<td>
The SAMLresponse Token base64 encoded
</td>
</tr>
</table>

</p></blockquote></details>

<details><summary><b>CheckSAMLToken</b> : Checks if the session is already SAML authenticated and if not computes a SAML AutnRequest</summary><blockquote><p>


## ![](https://github.com/convertigo/convertigo/blob/develop/engine/src/com/twinsoft/convertigo/beans/sequences/images/genericsequence_color_16x16.png?raw=true "GenericSequence") CheckSAMLToken

Checks if the session is already SAML authenticated and if not computes a SAML AutnRequest

<span style="color:DarkGoldenRod">Variables</span>

<table>
<tr>
<th>
name
</th>
<th>
comment
</th>
</tr>
<tr>
<td>
<img src="https://github.com/convertigo/convertigo/blob/develop/engine/src/com/twinsoft/convertigo/beans/variables/images/variable_color_16x16.png?raw=true "  alt="RequestableVariable" >&nbsp;CallingApplicationURL
</td>
<td>
The URL we should redirect to when Auth is completed
</td>
</tr>
<tr>
<td>
<img src="https://github.com/convertigo/convertigo/blob/develop/engine/src/com/twinsoft/convertigo/beans/variables/images/variable_color_16x16.png?raw=true "  alt="RequestableVariable" >&nbsp;SAMLEntityId
</td>
<td>
Our SP identity ID
</td>
</tr>
<tr>
<td>
<img src="https://github.com/convertigo/convertigo/blob/develop/engine/src/com/twinsoft/convertigo/beans/variables/images/variable_color_16x16.png?raw=true "  alt="RequestableVariable" >&nbsp;SAMLSsoServiceURL
</td>
<td>
The IDP service URL
</td>
</tr>
</table>

</p></blockquote></details>

<details><summary><b>GenerateAuthnRequest</b> : Utility to compute a AuthnRequest</summary><blockquote><p>


## ![](https://github.com/convertigo/convertigo/blob/develop/engine/src/com/twinsoft/convertigo/beans/sequences/images/genericsequence_color_16x16.png?raw=true "GenericSequence") GenerateAuthnRequest

Utility to compute a AuthnRequest. Can be signed if symbols lib_SAML.cert and lib_SAML.key.secret are defined.

<span style="color:DarkGoldenRod">Variables</span>

<table>
<tr>
<th>
name
</th>
<th>
comment
</th>
</tr>
<tr>
<td>
<img src="https://github.com/convertigo/convertigo/blob/develop/engine/src/com/twinsoft/convertigo/beans/variables/images/variable_color_16x16.png?raw=true "  alt="RequestableVariable" >&nbsp;IDPEntityID
</td>
<td>

</td>
</tr>
</table>

</p></blockquote></details>
</p></blockquote></details>

<details><summary><span style="color:DarkGoldenRod"><i>Rest Web Service</i></span></summary><blockquote><p>


## ![](https://github.com/convertigo/convertigo/blob/develop/engine/src/com/twinsoft/convertigo/beans/core/images/urlmapper_color_16x16.png?raw=true "UrlMapper") UrlMapper



<details><summary><span style="color:DarkGoldenRod"><i>Mappings</i></span></summary><blockquote><p>


### ![](https://github.com/convertigo/convertigo/blob/develop/engine/src/com/twinsoft/convertigo/beans/rest/images/pathmapping_color_16x16.png?raw=true "PathMapping") /SAML

The POST SAML Endpoint

<details><summary><span style="color:DarkGoldenRod"><i>Operations</i></span></summary><blockquote><p>


### ![](https://github.com/convertigo/convertigo/blob/develop/engine/src/com/twinsoft/convertigo/beans/rest/images/postoperation_color_16x16.png?raw=true "PostOperation") PostOperation



<span style="color:DarkGoldenRod">Parameters</span>

<table>
<tr>
<th>
name
</th>
<th>
comment
</th>
</tr>
<tr>
<td>
<img src="https://github.com/convertigo/convertigo/blob/develop/engine/src/com/twinsoft/convertigo/beans/rest/images/formparameter_color_16x16.png?raw=true "  alt="FormParameter" >&nbsp;RelayState
</td>
<td>
The SAML relaystate Value
</td>
</tr>
<tr>
<td>
<img src="https://github.com/convertigo/convertigo/blob/develop/engine/src/com/twinsoft/convertigo/beans/rest/images/formparameter_color_16x16.png?raw=true "  alt="FormParameter" >&nbsp;SAMLResponse
</td>
<td>
The SAML Token
</td>
</tr>
</table>


<span style="color:DarkGoldenRod">Responses</span>

<table>
<tr>
<th>
name
</th>
<th>
comment
</th>
</tr>
<tr>
<td>
<img src="https://github.com/convertigo/convertigo/blob/develop/engine/src/com/twinsoft/convertigo/beans/rest/images/operationresponse_color_16x16.png?raw=true "  alt="OperationResponse" >&nbsp;302-Response
</td>
<td>
Redirect
</td>
</tr>
</table>

</p></blockquote></details>
</p></blockquote></details>
</p></blockquote></details>
