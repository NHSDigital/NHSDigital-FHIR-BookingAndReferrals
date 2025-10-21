---
topic: senderonboarding
---

## {{page-title}}

API-M provides the [security model](https://digital.nhs.uk/developer/guides-and-documentation/security-and-authorisation/application-restricted-restful-apis-signed-jwt-authentication) for BaRS. 

To onboard as a sender follow these steps:

Step 1: follow the NHS Developer authenitication and authorisation process [NHS Developer authentication and authorisation](https://digital.nhs.uk/developer/guides-and-documentation/security-and-authorisation/user-restricted-restful-apis-nhs-login-separate-authentication-and-authorisation#step-1-register-your-application-with-nhs-login)

Step 2: trust the Certificate Authorities (CA) mentioned below. For INT this will be downloadable from http://pki.nhs.uk/int/G2/auth/NHSINTAuthG2.crt 
( you can examine the .cer file if you have one )
```
openssl x509 -in barsintreceiver.cer -text -noout
```


