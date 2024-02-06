## Sender

The BaRS standard uses an [application-restricted](https://digital.nhs.uk/developer/guides-and-documentation/security-and-authorisation#application-restricted-apis) security model and [security pattern](https://digital.nhs.uk/developer/guides-and-documentation/security-and-authorisation/application-restricted-restful-apis-signed-jwt-authentication#how-this-pattern-works) as opposed to a [user-restricted security](https://digital.nhs.uk/developer/guides-and-documentation/security-and-authorisation#user-restricted-apis) model. This means the application is authenticated as opposed to the end-user using it. The high level steps for a sending application are defined below:

1. The end user launches the calling application
2. Time passes, until the user needs to interact with BaRS 
3. The calling application generates and signs a JWT, using its own private key
4. The calling application calls our OAuth 2.0 token endpoint with the signed JWT. In particular, this uses the OAuth 2.0 client credentials flow
5. We check the signature against the application's public key and, if valid, return an access token to the calling application
6. The calling application calls the BaRS API, including the access token
7. The BaRS API allows the interaction should the access token be valid

<br>
<hr>