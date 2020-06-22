---
title: Configure TLS authentication with API Manager
linkTitle: Configure TLS authentication with API Manager
weight: 22
date: 2020-06-22
description: Configure API Portal and API Manager Mutual TLS authentication to increase your API Portal the level of security.

---
Configure API Portal and API Manager Mutual TLS authentication to increase security in API Portal and API Manager connection. The mutual authentication ensures that traffic is secure between the server (API Manager), which presents its certificate to the client, and the client (API Portal), which presents its own certificate for the server's verification.

Before you start you must have a TLS X.509 certificate, which presents the identity of API Portal to API Manager. To configure API Manager to require and verify this certificate, see [Set up the back-end SSL server for mutual authentication](/docs/apim_administration/apimgr_admin/api_mgmt_custom_policies/#set-up-the-back-end-ssl-server-for-mutual-authentication).

{{< alert title="Useful Tip" color="warning" >}}You can use the same TLS certificate that API Portal presents to the browser when being accessed.{{< /alert >}}

## Configure API Portal to present its certificate

1. Log in to the Joomla! Administrator Interface (JAI), and click **Components** > **API Portal** > **API Manager**.
2. There is a section called **Mutual Authentication** on this page.
3. Change the "Send API Portal Certificate to API Manager" to **Yes**.
4. "API Portal (Client) Certificate" - click "Choose File" and select the certificate file from your local file system. The supported file extensions for the certificate files are - **.cer**, **.crt**, **.pem**, **.der**
5. "API Portal (Client) Private key" - click "Choose File" and select the private key file for the certificate from your local file system. The supported file extensions for the private key is - **.key**
6. "Private Key Passphrase" - if your private key is passphrase protected, type your passphrase in the text field (the text is masked). Leave the field empty if no passphrase on your private key.
7. Click **Save**.

{{< alert title="Note" color="warning" >}}If you have multiple API Managers configured this API Portal (client) certificate will be present by the API Portal HTTP Client for every one of them. It's up to each API Manager whether to require and verify this certificate or not. No performance impact should be expected ! {{< /alert >}}

## General recommendation

Once you configure the API Manager to require client certificate, it means that every client that is connecting on port 8075 (or whatever default port is configured) will need to present its certificate. This includes not only API Portal as a client but the browser too. 

So, in order to avoid troubles with connecting to API Manager from the browser we recomend to expose a new port for connection with API Portal and configure API Manager to require client certificate for connection on this port and leave the default port (8075) in the same state as it was until now. For more details on how to expose a new port for API Manager please check - [Add Http or Https Interface.](/docs/apim_policydev/apigw_gw_instances/general_services/#http-and-https-interfaces)

Once you expose a new port, please don't forget to change it in the API Portal configuration - JAI > Components > API Portal > API Manager > **port** filed

With this type of configuration you will have a specific port for API Portal to connect to API Manager and a Mutual Authentication on it and the browser will continue to connect to API Manager on the default port (8075)