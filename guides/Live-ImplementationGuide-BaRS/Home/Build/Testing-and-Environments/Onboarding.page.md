---
topic: onboarding
---

## {{page-title}}

API-M provides the [security model](https://digital.nhs.uk/developer/guides-and-documentation/security-and-authorisation/application-restricted-restful-apis-signed-jwt-authentication) for BaRS. 

There are two roles: Sender and Receiver. Most BaRS Applications will require a solution to support both roles, despite being predominantly one or the other, because of the response workflow steps. In response flows, the original Sender becomes a Receiver and the original Receiver becomes a Sender. 

The Sender obtains a token from the API-M platform to make requests of the BaRS API Proxy, which brokers the request through the Receiver, secured via TLS-MA (Transport Layer Security-Mutual Authentication).

BaRS is based on internet-first principles and there is no requirement for [Health and Social Care Network (HSCN)](https://digital.nhs.uk/services/health-and-social-care-network) connectivity.

### Sender
* [Follow the steps here to get set up](https://digital.nhs.uk/developer/guides-and-documentation/security-and-authorisation/user-restricted-restful-apis-nhs-login-separate-authentication-and-authorisation#step-1-register-your-application-with-nhs-login)

The sender will also need to trust the Certificate Authorities mentioned below. For INT this will be downloadable from http://pki.nhs.uk/int/G2/auth/NHSINTAuthG2.crt 
( you can examine the .cer file if you have one )
```
openssl x509 -in barsintreceiver.cer -text -noout
```
### Some commands that might help to get the Root CA and chain

To get a cert from an endpoint
```
openssl s_client -showcerts -connect BaRS-INT-X26.BarsReceiver.thirdparty.nhs.uk:443 < /dev/null | openssl x509 -outform PEM > server-cert.pem
```
Then to list info from the .pem
```
openssl x509 -in server-cert.pem -text -noout
```

You can use the output from this command to get the full CA chain.

```
sudo cp ca-chain.pem /usr/local/share/ca-certificates/ sudo update-ca-certificates
```

This will ensure that your system trusts the certificates issued by the CA.


### Receiver 
BaRS will utilise TLS-MA to communicate with Receiving endpoints. Receiving endpoints will require a certificate under the NHS Root CA to facilitate TLS-MA.
    
* The receiver must request a certificate under the NHS Root CA
    * There are different certificate chains for INT and Prod
    * [INT Certificate](https://digital.nhs.uk/services/path-to-live-environments/integration-environment#rootca-and-subca-certificates) chains (**Note:** _these may be out of date_)
    * [Prod Certificate](https://digital.nhs.uk/services/path-to-live-environments/live-environment) chains (**Note:** _these may be out of date_)
* The receiving endpoint will present the certificate obtained for TLS-MA
* The receiving endpoint will need to trust the Root CAs and SubCAs for their respective environments
* The receiving endpoint will only accept requests presented with certificates from their respective chains

As the certificates are using the NHS Root CA, the FQDN must be an nhs.uk address. This is the case for both INT and Prod.

You can apply for your domain [here](https://digital.nhs.uk/services/networking-addressing/apply-for-an-nhs.uk-domain-for-websites-and-web-applications), ensuring that you complete Section 5: For website or application records visible on the public internet.

Once you have your domain registered, you can then begin the process to obtain your certificate by generating a certificate request.

Certificate requests will need to be signed for your endpoint. Note that the fully qualified domain (FQDN) name is equal to the certificate name (CN) by convention.

You need to create a Certificate Signing Request (*.csr). This is the file you will send to us so we can generate a signed certificate for your endpoints. The first step is to create a private key; a password is optional.
```
openssl genpkey -algorithm RSA -out private.key -aes256
```
Then, to create the *.csr, use the following command:</br>
**Note:** <small>_Generate the CSR with only the common name field populated, which must match the FQDN. All other fields can remain blank. The email field MUST be blank. Please note FQDNs MUST be in the .nhs.uk domain as we can only issue certificates in this domain._</small>
```
openssl req -new -key private.key -out request.csr
```

At this point, you should have a .key and a .csr file. The next step will be to send the .csr file to be signed by the NHS and get the client certificate. For full steps, see the sections below for each environment.

#### Integration (INT)
* [Request](https://digital.nhs.uk/services/path-to-live-environments/path-to-live-forms/combined-endpoint-and-service-registration-request) a ‘certificate only’ from ITOC
    * {{render:Onboarding FORM.png}}
    * Certificate Only (No endpoint)
    * Integration environment
    * FQDN must match your domain and CN on the cert e.g. '**BaRS-INT-\<ODS Code\>.\<Supplier name\>.thirdparty.nhs.uk**'
    * Ensure it is clear this is a request for a ‘BaRS’ certificate
    * ‘N/A’ in the Party Key section because there is no relation to SDS endpoints
* Receive certificate from ITOC
* Email <england.bookingandreferralstandard@nhs.net> with Receiver URL for BaRS/API-M to add to the Endpoint Catalogue

#### Production (Prod)
* Once Solution Assurance issues the supplier with the Technical Conformance certificate, Production endpoints can be requested
* Send the .csr to <dir@nhs.net>, indicating this is for a BaRS Receiver endpoint
    * Format for FQDN on PROD for:
        * Supplier hosted solutions is ‘**BaRS-PROD-\<ODS Code\>.\<Supplier name\>.thirdparty.nhs.uk**’
            * This option is used for multi-tenanted solutions.
        * Service Provider hosted solutions is ‘**BaRS-PROD-\<ODS Code\>.\<Provider name\>.nhs.uk**’
            * This option is used for non multi-tenanted solutions. If multiple endpoints are needed, the ODS code can be appended with an identifier for the setting.
            * It may be that the provider already has a 'nhs.uk' standard domain DNS entry. If one exists, it should be used for this new subdomain.
* Receive certificate from DIR Team
* Email <england.bookingandreferralstandard@nhs.net> with Receiver URL for BaRS/API-M to add to the Endpoint Catalogue

**Note:** <span style="color:red">**Receiver Firewall Amendments**</span> - Requests from the BaRS API Proxy will originate from **INT** on **35.197.254.55** & **35.246.55.143** and **PROD** on **34.89.0.111** & **34.89.69.6**.

Once you have the certificate from the NHS service desk, copy the text for the cert with the `-----BEGIN CERTIFICATE` as the first line and `END CERTIFICATE-----` as the last. Save this text locally as a file called barsinreceiver.cer (change the name to suit).

You will probably need to make a .pfx file so you can serve HTTPS (TLS) endpoints. You can use the command below to export a *.pfx file from the *.key file you made earlier (when you made the *.csr file) along with the *.cer file you were emailed.

```
openssl pkcs12 -export -out barsintreceiver.pfx -inkey barsintreceiver.key -in barsintreceiver.cer
```

You will be prompted for a password for your .pfx file. You will need to use this password along with the .pfx file.

Once you have the *.pfx file you can use it the following way (C# example, Other launguages will vary but be similar)

``` c#

// Configure Kestrel to use the certificate
builder.WebHost.ConfigureKestrel(options =>
{
    options.ListenAnyIP(8080, listenOptions =>
    {
        listenOptions.UseHttps(certPath, certPassword);
    });
});

```