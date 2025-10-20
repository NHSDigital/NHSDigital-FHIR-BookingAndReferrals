---
topic: onboarding
---

## {{page-title}}

In each BaRS workflow there are two roles: Sender and Receiver. In applications with response workflows, both parties act as a Sender and a Receiver, and will need to follow the instructions to onboard as both. 

The Sender obtains a token from the API-M platform to make requests of the BaRS API Proxy, which brokers the request through the Receiver, secured via TLS-MA (Transport Layer Security-Mutual Authentication).

BaRS is based on internet-first principles and there is no requirement for [Health and Social Care Network (HSCN)](https://digital.nhs.uk/services/health-and-social-care-network) connectivity.

### Sender Onboarding

API-M provides the [security model](https://digital.nhs.uk/developer/guides-and-documentation/security-and-authorisation/application-restricted-restful-apis-signed-jwt-authentication) for BaRS. 

To onboard as a sender follow these steps:

Step 1: follow the NHS Developer authenitication and authorisation process [NHS Developer authentication and authorisation](https://digital.nhs.uk/developer/guides-and-documentation/security-and-authorisation/user-restricted-restful-apis-nhs-login-separate-authentication-and-authorisation#step-1-register-your-application-with-nhs-login)

Step 2: trust the Certificate Authorities (CA) mentioned below. For INT this will be downloadable from http://pki.nhs.uk/int/G2/auth/NHSINTAuthG2.crt 
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


### Receiver Onboarding
BaRS will utilise TLS-MA to communicate with Receiving endpoints. Receiving endpoints will require a certificate under the NHS Root CA to facilitate TLS-MA.  The receiver will need to follow these steps for Integration and Production environments.

To onboard as a receiver follow these steps:

Step 1: Apply for your domain [apply for a new nhs.uk domain](https://digital.nhs.uk/services/networking-addressing/apply-for-an-nhs.uk-domain-for-websites-and-web-applications).  You must complete Section 5: For website or application records visible on the public internet.

Step 2: Request a certificate under the NHS Root CA. The FQDN must be an nhs.uk address.
    * There are different certificate chains for INT and Prod
    * [INT Certificate](https://digital.nhs.uk/services/path-to-live-environments/integration-environment#rootca-and-subca-certificates) chains (**Note:** _these may be out of date_)
    * [Prod Certificate](https://digital.nhs.uk/services/path-to-live-environments/live-environment) chains (**Note:** _these may be out of date_)stered, you can then begin the process to obtain your certificate by generating a certificate request.
The fully qualified domain name (FQDN) is equal to the certificate name (CN) by convention.

Step 3: Create a Certificate Signing Request (*.csr). This is the file you will send to us so we can generate a signed certificate for your endpoints. Create a private key; a password is optional.
```
openssl genpkey -algorithm RSA -out private.key -aes256
```
Create the *.csr, use the following command:</br>
**Note:** <small>_Generate the CSR with only the common name field populated, which must match the FQDN. All other fields can remain blank. The email field MUST be blank. Please note FQDNs MUST be in the .nhs.uk domain as we can only issue certificates in this domain._</small>
```
openssl req -new -key private.key -out request.csr
```

Step 4: Send the .csr file to be signed by the NHS and get the client certificate. To do this, follow these environment specific steps:

#### Client certificate: Integration (INT)
Step 1: Contact ITOC to make a [Combined endpoint and service registration request](https://digital.nhs.uk/services/path-to-live-environments/path-to-live-forms/combined-endpoint-and-service-registration-request) 
     {{render:Onboarding FORM.png}}
    In the form:
    * Select Create/renew a certificate only (No endpoint)
    * Specify Integration environment
    * FQDN must match your domain and CN on the cert e.g. '**BaRS-INT-\<ODS Code\>.\<Supplier name\>.thirdparty.nhs.uk**'
    * In Additional comments/notes, state ‘BaRS’ certificate request
    * Add ‘N/A’ in the Party Key field because there is no relation to SDS endpoints
Step 2: Receive certificate from ITOC
Step 3: Email <england.bookingandreferralstandard@nhs.net> with Receiver URL for BaRS/API-M to add to the Endpoint Catalogue

#### Client certificate: Production (Prod)
Production endpoints can only be requested when Solution Assurance issue the supplier with the Technical Conformance certificate, 
Step1: Send the .csr to <dir@nhs.net>, indicating this is for a BaRS Receiver endpoint
    * Format for FQDN on PROD for:
        * Supplier hosted solutions is ‘**BaRS-PROD-\<ODS Code\>.\<Supplier name\>.thirdparty.nhs.uk**’
            * This option is used for multi-tenanted solutions.
        * Service Provider hosted solutions is ‘**BaRS-PROD-\<ODS Code\>.\<Provider name\>.nhs.uk**’
            * This option is used for non multi-tenanted solutions. If multiple endpoints are needed, the ODS code can be appended with an identifier for the setting.
            * It may be that the provider already has a 'nhs.uk' standard domain DNS entry. If one exists, it should be used for this new subdomain.
Step 2: Receive certificate from DIR Team
Step 3: Email <england.bookingandreferralstandard@nhs.net> with Receiver URL for BaRS/API-M to add to the Endpoint Catalogue

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