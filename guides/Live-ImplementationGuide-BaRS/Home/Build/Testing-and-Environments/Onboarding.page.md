---
topic: onboarding
---

## {{page-title}}

API-M provide the [security model](https://digital.nhs.uk/developer/guides-and-documentation/security-and-authorisation/application-restricted-restful-apis-signed-jwt-authentication) for BaRS. 

There are two roles; Sender and Receiver, and most BaRS Applications will require a solution to support both, despite being predominantly one or the other, because of the response workflow steps. In responses flows, the original Sender becomes and Receiver and original Receiver becomes a Sender. 

The Sender obtains a token from the API-M platform to make requests of the BaRS API Proxy which brokers the request through the Receiver, secure via TLS-MA (Transport Layer Security-Mutual Authentication).

BaRS is based on internet-first principles and there is no requirement for [Health and Social Care Network (HSCN)](https://digital.nhs.uk/services/health-and-social-care-network) connectivity.

### Sender
Prerequiste steps to follow - 
* [Create Developer account](https://digital.nhs.uk/developer) click Create account
* Sign in, select **environment access** from the top
{{render:Onboarding Dev Account Title.png}}

* create a team by selecting "**My teams**", and then "**+ New Team**":

{{render:Onboarding Dev Account.png}}

* Assign members to your Team
* Create an App
    * Owner of the App should be the Team created above
    * You will need a callback URL (bottom of page)
    * Enable or request the API's you wish to use for your application
        * "Booking and Referral FHIR API (Sandbox Environment)" - for Sandbox
        * "Booking and Referral FHIR API (Integration Testing Environment)" - for INT
    * Generate an API Key for your application
* Define your **Key Identifier (KID)** to be used within your JWTs
    * KID Naming Convention (Development Systems) - **\<Supplier\>-\<Environment\>-\<rotation\>** i.e. **MySupplier-INT-1**
    * KID Naming Convention (Provider Systems) - **\<Provider\>-\<Environment\>-\<rotation\>** i.e. **Provider-INT-1**
* Generate a key pair (.pem)
    * [Windows based apps](https://phoenixnap.com/kb/generate-ssh-key-windows-10)
    * Alternatively, this [website](https://travistidwell.com/jsencrypt/demo/) can also generate Key Pairs
* Provide details to register your key
    * For INT : Register Public key with API Management
        * Email - <api.management@nhs.net> with:
            * Environment - Sandbox, Development, Integration Test or Production
            * App ID and Name from the portal
            * Public key
                * As an attachment, PEM-Encoded
            * The KID you have defined for this public key
            * APIs you want to use
    * For Production (each provider needs their own key).
        * Email - 
            * Specify Live
            * App ID and Name from the portal for both Production and the INT Suppliers Development environment.
            * Public key for the providers Production instance.
                * As an attachment, PEM-Encoded.
            * The KID defined for this public key.
            * The APIs you want to use.
* Generate a signed JWT using your private key
    * The header:
        * alg: The algorithm used
        * typ: "JWT" in this instance
        * kid: Your KID as provided to API Management above
        * example:

        ~~~json
                {
                    "alg":"RS512"
                    "typ":"JWT"
                    "kid":"BaRS-Sandbox-1"
                }
        ~~~

    * The payload:
        * iss: The API Key you generated in the portal
        * sub: The API Key you generated in the portal
        * aud: The full URL of the endpoint you are calling (example: https://sandbox.api.service.nhs.uk/oauth2/token )
        * jti: UUID/GUID, different for each request
        * exp: Epoch time, to be no more than 5 minutes in the future, indicating when your token will expire
        * example:

        ~~~json
                {
                    "iss":"IwrOdg62kM9LN1oFhlHAhWPHAhWPbV62",
                    "sub":"IwrOdg62kM9LN1oFhlHAhWPHAhWPbV62",
                    "kid":"BaRS-Sandbox-1",
                    "aud":"https://sandbox.api.service.nhs.uk/oauth2/token",
                    "jti":"b7ae4c12-3c04-465a-8877-c2e80f0126a3"
                    "exp":"1635263528"
                }
        ~~~

    * **Post** your JWT to the OAuth endpoint to receive a Token
        * **Note**: A token is not required for the Sandbox environment
        * Your request body should be **x-www-form-urlencoded** with the following fields
            * grant_typegrant_type = "client_credentials"
            * client_assertion_type = "urn:ietf:params:oauth:client-assertion-type:jwt-bearer"
            * client_assertion = \<Your signed JWT\>
            * example:

            ~~~
                curl --location --request POST 'https://sandbox.api.service.nhs.uk/oauth2/token' \
                --header 'Content-Type: application/x-www-form-urlencoded' \
                --data-urlencode 'grant_type=client_credentials' \
                --data-urlencode 'client_assertion_type=urn:ietf:params:oauth:client-assertion-type:jwt-bearer' \
                --data-urlencode 'client_assertion=eyJ0eXAiOiJKV1QiLCJraWQiOiJCYVJTLVNhbmRib3gtMSIsImFsZyI6IlJTNTEyIn0.
                eyJpc3MiOiJJd3JPZGc2MmtNOUxOMW9GaGw4UnlVUmJIQWhXUFY2MiIsInN1YiI6Ikl3ck9kZzYya005TE4xb0ZobDhSeVVSYkhBaFdQVjYyIiwia2lkIjoiQmFSUy1TYW5kYm94LTEiLCJhdWQiOiJodHRwczovL3NhbmRib3guYXBpLnNlcnZpY2UubmhzLnVrL29hdXRoMi90b2tlbiIsImp0aSI6IlQtWjdhTm1UODUybE1uVGtZb1NaRiIsImlhdCI6MTYzNTI2MjI2MiwibmJmIjoxNjM1MjYyMjYyLCJleHAiOjE2MzUyNjI1NjZ9.aUQSqvkzjAMRR21lNiE6YnksynPWx9wkXdEFJZ_muzGfeyuS3ooh-uXlOccQFSDS790Wrne49vMsf72NILK3iDjWyH2z8D8R_B_xYy2e3ZOktqQFNx5vZ0svC-_v1ranJKJJU8NiQog7JvRtXNwKcdExpge2bkhV2JN3bQtzPY0F7CxPohILmCIUvi3yEyr-nm3kxdB8LkifQAz132qpuO_1iENGmbqUgASYBZMTQIdD4aO8Vv9sJ9rvyIQyniw_DeY6SEMx4CHDiEb0NWmcOmpdBS1DDkuMiUohSpz8OXEYR1cZcL27dyibDJBY57FGCMBn1AVb43olYSumOIwg'

            ~~~
    * The expected **success** response from the Post should be a status 200 with a 3 field JSON response:
        * access_token: Your access token
        * expires_in: When it expires
        * token_type: "Bearer"
        * issued_at: Time issued
        * example: 

        ~~~json
                {
                    'access_token': 'Sr5PGv19wTEHJdDr2wx2f7IGd0cw',
                    'expires_in': '599',
                    'token_type': 'Bearer'
                    'issued_at': '1675784384503'
                }
        ~~~

    * A **failure** response will have a response code appropriate for the reason and the following 3 fields:
        * error: The error thrown
        * error_description: Diagnostics text to tell you why the error was thrown
        * message_id: A unique id for the interaction
        * example: 

        ~~~json
                {
                    "error": "public_key error",
                    "error_description": "You need to register a public key to use this authentication method - please contact support to configure",
                    "message_id": "rrt-8923968319386160140-b-geu2-23765-558685-1"
                }
        ~~~

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
