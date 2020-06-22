---
title: Mutual TLS Authentication with API Manager
description: Configure API Portal to send its own (client) certificate to API Manager
---
Before you start you should have a TLS certificate in X.509 format that will be used for the connection with API Manager. This certificate will serve to present the identity of API Portal to API Manager (Client side authentication). API Manager can be configured to require and verify this certificate (identity). 

{{< alert title="Useful Tip" color="warning" >}}You can use the same TLS certificate that API Portal presents to the browser when being accessed.{{< /alert >}}

## Configure API Portal to present its certificate

1. Log in to the Joomla! Administrator Interface (JAI), and click **Components** > **API Portal** > **API Manager**.
2. There is a section called **Mutual Authentication** on this page. 
3. Change the "Send API Portal Certificate to API Manager" to **Yes**.
4. "API Portal (Client) Certificate" - click "Choose File" and select the certificate file from your local file system.

{{< alert title="Important" color="warning" >}}The supported file extensions for the certificate files are - **.cer**, **.crt**, **.pem**, **.der** {{< /alert >}}

5. "API Portal (Client) Private key" - click "Choose File" and select the private key file for the certificate from your local file system.

{{< alert title="Important" color="warning" >}}The supported file extensions for the private key is - **.key** {{< /alert >}}
 

6. "Private Key Passphrase" - if your private key is passphrase protected, type your passphrase in the text field (the text is masked). Leave the field empty if no passphrase on your private key. 
7. Click **Save**.


## General recomendation 

Once you configure the API Manager to require client certificate, it means that every client that is connecting on port 8075 (or whatever default port is configured) will need to present its certificate. This includes not only API Portal as a client but the browser too. 

So, in order to avoid troubles with connecting to API Manager from the browser we recomend to expose a new port for connection with API Portal and configure API Manager to require client certificate for connection on this port and leave the default port (8075) in the same state as it was until now.

Once you expose a new port, please don't forget to change it in the API Portal configuration - JAI > Components > API Portal > API Manager > **port** filed

With this type of configuration you will have a specific port for API Portal to connect to API Manager and a Mutual Authentication on it and the browser will continue to connect to API Manager on the default port (8075)