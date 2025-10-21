---
topic: Connect-as-a-receiver
---

## {{page-title}}

BaRS uses TLS-MA to communicate with Receiving endpoints. Receiving endpoints need a certificate under the NHS Root CA to facilitate TLS-MA.  The receiver needs to follow these steps to access Integration (INT) and Production (PROD) environments.

To connect to the BaRS proxy as a receiver follow these steps:

Step 1: Apply for your domain [apply for a new nhs.uk domain](https://digital.nhs.uk/services/networking-addressing/apply-for-an-nhs.uk-domain-for-websites-and-web-applications).  You must complete Section 5: For website or application records visible on the public internet.

Step 2: Request a certificate under the NHS Root CA. The FQDN must be an nhs.uk address.
    * There are different certificate chains for INT and PROD
    * [INT Certificate](https://digital.nhs.uk/services/path-to-live-environments/integration-environment#rootca-and-subca-certificates) chains (**Note:** _these may be out of date_)
    * [PROD Certificate](https://digital.nhs.uk/services/path-to-live-environments/live-environment) chains (**Note:** _these may be out of date_)stered, you can then begin the process to obtain your certificate by generating a certificate request.
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

Step 4: Send the .csr file to be signed by NHS England and get the client certificate. To do this, follow these environment specific steps:

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

#### Client certificate: Production (PROD)
**Production endpoints can only be requested when Solution Assurance issue the supplier with the Technical Conformance certificate** 
Step1: Send the .csr to <dir@nhs.net>, indicating this is for a BaRS Receiver endpoint
    * Format for FQDN on PROD for:
        * Supplier hosted solutions is ‘**BaRS-PROD-\<ODS Code\>.\<Supplier name\>.thirdparty.nhs.uk**’
            * This option is used for multi-tenanted solutions.
        * Service Provider hosted solutions is ‘**BaRS-PROD-\<ODS Code\>.\<Provider name\>.nhs.uk**’
            * This option is used for non multi-tenanted solutions. If multiple endpoints are needed, the ODS code can be appended with an identifier for the setting.
            * It may be that the provider already has a 'nhs.uk' standard domain DNS entry. If one exists, it should be used for this new subdomain.
Step 2: Receive certificate from DIR Team
Step 3: Email <england.bookingandreferralstandard@nhs.net> with Receiver URL for BaRS/API-M to add to the Endpoint Catalogue
Step 4: Make changes to your [firewall exceptions](https://simplifier.net/guide/nhsbookingandreferralstandard/Home/Deploy/Technical-deployment\Firewallexceptions) to receive messages from the BaRS proxy.

#### Installing and configuring your application to use the certificate
Step 1: INT and PROD copy the cert text inlcuding `-----BEGIN CERTIFICATE` as the first line and `END CERTIFICATE-----` as the last. Save this text locally as a file called barsinreceiver.cer (change the name to suit).

Step 2: Create a .pfx file so you can serve HTTPS (TLS) endpoints. You can use the command below to export a *.pfx file from the *.key file you made earlier (when you made the *.csr file) along with the *.cer file you were emailed.

```
openssl pkcs12 -export -out barsintreceiver.pfx -inkey barsintreceiver.key -in barsintreceiver.cer
```

Step 3: Create a password for your .pfx file. 

Step 4: Make configuration changes to reference the *.pfx file and password

(C# example, Other launguages will vary but be similar)

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

