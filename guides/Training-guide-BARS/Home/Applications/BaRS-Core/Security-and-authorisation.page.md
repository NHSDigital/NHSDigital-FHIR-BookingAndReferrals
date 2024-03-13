# {{page-title}}

## Sender

The BaRS standard uses an [application-restricted](https://digital.nhs.uk/developer/guides-and-documentation/security-and-authorisation#application-restricted-apis) security model and [security pattern](https://digital.nhs.uk/developer/guides-and-documentation/security-and-authorisation/application-restricted-restful-apis-signed-jwt-authentication#how-this-pattern-works) as opposed to a [user-restricted security](https://digital.nhs.uk/developer/guides-and-documentation/security-and-authorisation#user-restricted-apis) model. This means the application is authenticated as opposed to the end-user using it. The high level steps for a sending application are defined below:

1. The end user launches the calling application
2. Time passes, until the user needs to interact with BaRS 
3. The calling application generates and signs a JWT, using its own private key
4. The calling application calls our OAuth 2.0 token endpoint with the signed JWT. In particular, this uses the OAuth 2.0 client credentials flow
5. We check the signature against the application's public key and, if valid, return an access token to the calling application
6. The calling application calls the BaRS API, including the access token
7. The BaRS API allows the interaction should the access token be valid

## OAuth Endpoints

| Environment      | Endpoint                                  | Usage/Availability                                         |
|------------------|-------------------------------------------|------------------------------------------------------------|
| Sandbox          | https://sandbox.api.service.nhs.uk/oauth2 | Authentication is not required in the Sandbox environment. |
| Development      | https://dev.api.service.nhs.uk/oauth2     | Limited to specific APIs                                   |
| Integration test | https://int.api.service.nhs.uk/oauth2     | All APIs                                                   |
| Production       | https://api.service.nhs.uk/oauth2         | All APIs                                                   |

## Receiver

BaRS will utilise TLS-MA (Mutual Authentication) to communicate with receiving endpoints. Receiving endpoints will require a certificate under the NHS Root CA to facilitate TLS-MA.

- The receiver will need to request a certificate under the NHS Root CA
    - There are two different certificate chains for INT and Prod
    - INT Certificate chains can be found here: https://digital.nhs.uk/services/path-to-live-environments/integration-environment#rootca-and-subca-certificates
    - Prod Certificate chains can be found here: https://digital.nhs.uk/services/path-to-live-environments/live-environment

- The receiving endpoint will present the certificate obtained for TLS-MA
- The receiving endpoint will need to trust the Root CAs and SubCAs for their respective environments
- The receiving endpoint will only accept requests presented with certificates from their respective chains

As the certificates are using the NHS Root CA, fully qualified domain name (FQDN) must be an nhs.uk address, this is the case for both INT and Prod

You need to [apply for your domain](https://digital.nhs.uk/services/networking-addressing/apply-for-an-nhs.uk-domain-for-websites-and-web-applications), ensuring that you complete 'Section 5: For website or application records visible on public internet'.

In production there is a naming convention that must be adhered to. In INT the naming convention should be adhered where possible. In the context of BaRS an example will be:

- ==BaRS-< ODSCode >.< OrganisationName >.nhs.uk== , BaRS is always the application name.

Once you have you have your domain registered you can then begin the process to obtain your certificate by generating a certificate request.

Certificate requests will need to be signed for your endpoint. Note that the FQDN is equal to the certificate name (CN) by convention.

At this point you should have a .key and a .csr files. The next step will be to send the .csr file to be signed by the NHS and get the client certificate.

- If your client certificate will be implemented in any PTL environment then you should send the .csr file to [itoc.supportdesk@nhs.net](mailto:itoc.supportdesk@nhs.net) and they will reply with the certificate (.crt file)

- If your client certificate will be implemented in the PROD environment then the .csr file needs to be send to the DIR team at [dir@nhs.net](mailto:dir@nhs.net) and they will take care of issuing the certificate after validating your request with the Live Services Pipeline at  [liveservices.gate@nhs.net](mailto:liveservices.gate@nhs.net)

## Authorisation

BaRS will use several HTTP headers to facilitate authorisation. Although optional, receivers can expect these to be present for each request (excluding /metadata and /MessageDefinition), where applicable, to enforce access control. These will be in addition to the X-Request-ID and the X-Correlation-ID headers. If the information in these headers is available in the sending system, they'll be included in the request.

Each of these HTTP headers are objects and will therefore need to be added in the form of a standard Base64 encoded string.

Examples of each HTTP header item can be found within the [API Specification](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_0_0#get-/Appointment).

| HTTP Header                  | Purpose                                                                                                                                                                                                                  |
|------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| NHSD-End-User-Organisation   | This will represent the organisation making the request. It Shall include the ODS code and the human readable name of the organisation making the request. The object is based on a FHIR organisation resource.          |
| NHSD-Request-Person          | This entry will represent the Person sending the request.                                                                                                                                                                |
| NHSD-Requesting-Practitioner | This entry will represent the Practitioner associated to the request. It shall include their sds role id and a SNOMED code related to their role where applicable.  The object is based on a FHIR Organisation resource. |
| NHSD-Requesting-Software     | This entry will represent the Software or application making the request. It shall include an identifier for the instance, the product name and its version. The object is based on a FHIR Device resource.              |

<hr>