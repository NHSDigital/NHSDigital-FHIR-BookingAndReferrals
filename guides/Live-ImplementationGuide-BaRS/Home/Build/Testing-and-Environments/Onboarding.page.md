---
topic: onboarding
---

## {{page-title}}

API-M provide the [security model](https://digital.nhs.uk/developer/guides-and-documentation/security-and-authorisation/application-restricted-restful-apis-signed-jwt-authentication) for BaRS. 

There are two roles; Sender and Receiver, and most BaRS Applications will require a solution to support both, despite being predominantly one or the other, because of the response workflow steps. In responses flows, the original Sender becomes and Receiver and original Receiver becomes a Sender. 

The Sender obtains a token from the API-M platform to make requests of the BaRS API Proxy which brokers the request through the Receiver, secure via TLS-MA (Transport Layer Security-Mutual Authentication).

BaRS is based on internet-first principles and there is no requirement for [Health and Social Care Network (HSCN)](https://digital.nhs.uk/services/health-and-social-care-network) connectivity.

### Sender
* [Follow the steps here](https://digital.nhs.uk/developer/guides-and-documentation/security-and-authorisation/user-restricted-restful-apis-nhs-login-separate-authentication-and-authorisation#step-1-register-your-application-with-nhs-login)

### Receiver 
BaRS will utilise TLS-MA to communicate with Receiving endpoints. Receiving endpoints will require a certificate under the NHS Root CA to facilitate TLS-MA.
    
* The receiver must request a certificate under the NHS Root CA
    * There are different certificate chains for INT and Prod
    * [INT Certificate](https://digital.nhs.uk/services/path-to-live-environments/integration-environment#rootca-and-subca-certificates) chains
    * [Prod Certificate](https://digital.nhs.uk/services/path-to-live-environments/live-environment) chains
* The receiving endpoint will present the certificate obtained for TLS-MA
* The receiving endpoint will need to trust the Root CAs and SubCAs for their respective environments
* The receiving endpoint will only accept requests presented with certificates from their respective chains


As the certificates are using the NHS Root CA, FQDN must be an nhs.uk address, this is the case for both INT and Prod

You can apply for your domain [here](https://digital.nhs.uk/services/networking-addressing/apply-for-an-nhs.uk-domain-for-websites-and-web-applications), ensuring that you complete Section 5: For website or application records visible on public internet

Once you have you have your domain registered you can then begin the process to obtain your certificate by generating a certificate request

Certificate requests will need to be signed for your endpoint. Note that the fully qualified domain (FQDN) name is equal to the certificate name (CN) by convention

At this point you should have a .key and a .csr files. The next step will be to send the .csr file to be signed by the NHS and get the client certificate. For full steps see below sections for each environment under 'Configuring endpoints for different environments'

* If your client certificate will be implemented in any PTL environment then you should send the .csr file to <itoc.supportdesk@nhs.net> 
* If your client certificate will be implemented in the PROD environment then the .csr file needs to be sent to the DIR team at <dir@nhs.net> and they will issue the certificate after validating your request with the Live Services Pipeline at <liveservices.gate@nhs.net>

#### Integration (INT)
* [Request](https://digital.nhs.uk/services/path-to-live-environments/path-to-live-forms/combined-endpoint-and-service-registration-request) a ‘certificate only’ from ITOC
    * {{render:Onboarding FORM.png}}
    * Certificate Only (No endpoint)
    * Integration environment
    * Format for **development** systems FQDN on INT is ‘**BaRS-INT-\<ODS Code\>.\<Supplier name\>.thirdparty.nhs.uk**’
    * Format for **provider** systems FQDN on INT is ‘**BaRS-INT-\<ODS Code\>.\<Provider name\>.nhs.uk**’
    * Ensure it is clear this is a request for a ‘BaRS’ certificate
    * ‘N/A’ in the Party Key section because there is no relation to SDS endpoints
    * In the .csr, the ‘email’ field must be blank
* Receive certificate from ITOC
* Email <dnsteam@nhs.net> with FQDN and **public facing IP** to register DNS
* Email <bookingandreferralstandard@nhs.net> with Receiver URL for BaRS/API-M to add to the Endpoint Catalogue

#### Production (Prod)
* Once Solution Assurance issue the supplier with the Technical Conformance certificate Production endpoints can be requested
* Sends .csr to <dir@nhs.net>, indicating this is for a BaRS Receiver endpoint
    * Format for FQDN on PROD for -
        * Supplier hosted solutions is ‘**BaRS-PROD-\<ODS Code\>.\<Supplier name\>.thirdparty.nhs.uk**’
            * This option is used for multi-tenanted solutions.
        * Service Provider hosted solutions is ‘**BaRS-PROD-\<ODS Code\>.\<Provider name\>.nhs.uk**’
            * This option is used for non multi-tenanted solutions. If multiple endpoints are needed, the ODS code can be appended with an identifier for the setting.
            * It may be that the provider already has a 'nhs.uk' standard domain DNS entry, If one exists, it should be used for this new subdomain.
* Receive certificate from DIR Team
* Email <dnsteam@nhs.net> with FQDN and **public facing IP** to register DNS
* Email <bookingandreferralstandard@nhs.net> with Receiver URL for BaRS/API-M to add to the Endpoint Catalogue

**Note** - <span style="color:red">**Receiver Firewall Amendments**</span> - Requests from the BaRS API Proxy will originate from **INT** on **35.197.254.55** & **35.246.55.143** and **PROD** on **34.89.0.111** & **34.89.69.6**
