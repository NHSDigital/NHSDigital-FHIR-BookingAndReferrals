---
topic: connect-as-a-sender
---

## {{page-title}}

APIM provides the [security model](https://digital.nhs.uk/developer/guides-and-documentation/security-and-authorisation/application-restricted-restful-apis-signed-jwt-authentication) for BaRS. 

To connect to the BaRS proxy as a sender follow these steps:

Step 1: follow the NHS Developer authentication and authorisation process [NHS Developer authentication and authorisation](https://digital.nhs.uk/developer/guides-and-documentation/security-and-authorisation/user-restricted-restful-apis-nhs-login-separate-authentication-and-authorisation#step-1-register-your-application-with-nhs-login)

Step 2: trust the Certificate Authorities (CA) mentioned below. For INT this will be downloadable from http://pki.nhs.uk/int/G2/auth/NHSINTAuthG2.crt 
( you can examine the .cer file if you have one )
```
openssl x509 -in barsintreceiver.cer -text -noout
```

Step 3: The above steps enables access to the APIM platform. To authorise the access to the BaRS Proxy (which is hosted on the APIM Platform), you must provide the following to the BaRS Team (via email <england.bookingandreferralstandard@nhs.net>):

* App Name* 
* App ID (PROD)* 
* App ID (INT) (both App IDs are needed to connect to PROD)*
* App Description*
* Name of the Organisation
* ODS code of the Organisation
* Product Name (as stated in the SCAL or TCC)
* JWKS resource URL (if self hosting)
* KID for JWKS (if APIM host and defined in earlier steps)
* Public key (if APIM host and generated in earlier steps)

The starred (\*) items can be found by logging into the [Digital Onboarding Service](https://onboarding.prod.api.platform.nhs.uk) and selecting 'Environment access' under the *Introduction and onboarding* section.