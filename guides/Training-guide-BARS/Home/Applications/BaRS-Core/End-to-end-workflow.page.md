---
topic: core-EndToEndWorkflow
---

# {{page-title}}

This section covers the core elements of workflow outlined within the Booking and Referral Standard. There are two caveats when reading this:

- Workflow is dependent on its Application or use case, for example in 999 - CAS validation, there is no step to perform a booking. See the relevant use case page in the 
{{pagelink:applications, text:BaRS Applications}} section. 


- The order of workflow is interchangeable. It is possible to:
    - make a referral before a booking
    - refer without booking
    - book without referring


<a href="https://raw.githubusercontent.com/NHSDigital/booking-and-referral-media/master/src/images/WorkFlows/CoreWorkflowBaRS-1.0.0.svg" target="_blank"><img src="https://raw.githubusercontent.com/NHSDigital/booking-and-referral-media/master/src/images/WorkFlows/CoreWorkflowBaRS-1.0.0.svg" width="1200"></img></a>


## Service discovery 

For a sender making a booking or referral, the first step is to establish a service (including the identifier) to send to. This can be achieved by using national or local service directories or preconfigured services, where a sender only ever sends to a handful of endpoints. The service identifier is all the sender requires to engage with a service which supports BaRS. {{pagelink:Home/Helpandsupport, text:Contact us}}  if you need further information about service discovery.

## Authenticate with BaRS

The sender must have already [connected with our platform](https://digital.nhs.uk/developer/guides-and-documentation/security-and-authorisation/application-restricted-restful-apis-signed-jwt-authentication) in order to generate an access token to make a request of the BaRS API. The sender generates and signs a JWT and sends this request to the BaRS token endpoint which provides an access token to be used to interact with the BaRS API. 
A receiver will follow the same process to interact with BaRS API when providing feedback to an original sender, for example. The sender and receiver switch roles in the workflow for referral in both the current first-of-type use cases. This is only relevant to some Applications and will be detailed in the specific {{pagelink:Home/Design/BaRS-Applications/Applications , text:application guide.}}

## BaRS FHIR API

The [BaRS FHIR API](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_0_0) supports all functionality with receiver APIs for both booking and referrals. Once an access token has been obtained, the sender can start making requests of the API. 

Note: With every API request the sender must include the HTTP header parameter 'NHSD-Target Identifier'. 

You can find details for each endpoint in the [API Specification](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_0_0). 

## HTTP header

The BaRS API specifies several additional headers, many of which are items described in a standard Base64 encoded object (JSON). Their purpose and usage are described below. Examples can be found in the [API Specification](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_0_0). 

## Routing

| Header                 | Requirement            | Description                                                  | Value                      |
|------------------------|------------------------|--------------------------------------------------------------|----------------------------|
| NHSD-Target-Identifier | Required by the sender | Allows BaRS to route the message to the appropriate endpoint | Base64 encoded JSON object |

## Authentication and Authorisation

| Header                       | Requirement                                              | Description                                                                                                                                                                                                                         | Value                                                       |
|------------------------------|----------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------|
| Authorisation                | Required by the sender and not forwarded to the receiver | Will contain a token obtained from the relevant OAuth endpoint for the BaRS API being called. This token facilitates authentication with the API.                                                                                   | String representing a token                                 |
| NHSD-End-User- Organisation  | Optional for the sender and forwarded to the receiver    | For authorisation purposes this header contains information about the organisation making the request. Can be used by the receiver to impose access control limitations and should be retained for auditing purposes.               | Base64 encoded object based on a FHIR Organization resource |
| NHSD-Requesting-Person       | Optional for the sender and forwarded to the receiver    | For authorisation purposes this header contains information about the individual initiating the request itself. This can be used by the receiver to impose access control limitations and should be retained for auditing purposes. | Base64 encoded object based on a FHIR Person resource       |
| NHSD-Requesting-Practitioner | Optional for the sender and forwarded to the receiver    | For authorisation purposes this header contains information about the healthcare professional making the request. Can be used by the receiver to impose access control limitations and should be retained for auditing purposes.    | Base64 encoded object based on a FHIR Practitioner resource |
| NHSD-Requesting-Software     | Optional for the sender and forwarded to the receiver    | For authorisation purposes this header contains information about the  application making the request. This can be used by the receiver to impose access control limitations and should be retained for auditing purposes.          | Base64 encoded object based on a FHIR Device resource       |

### Transactional integrity

| Header           | Requirement                                                       | Description                                                               | Value  |
|------------------|-------------------------------------------------------------------|---------------------------------------------------------------------------|--------|
| X-Request-ID     | Required for sending of any request and forwarded to the receiver | Will facilitate transactional integrity and the ability to audit messages | UUID   |
| X-Correlation-Id | Required for sending of any request and forwarded to the receiver | Will facilitate transactional integrity and the ability to audit messages | UUID   |

We expect receivers to use and store the header values in the following ways:

- to ensure the message maintains transactional integrity and hasn't been received previously 
- to check who has sent the request and apply access control if desired
- to ensure all interactions are auditable

If at any point the request fails, the receiver must send an appropriate error response (see Error handling) back to the sender to inform them why the request cannot be fulfilled. It is important to return as accurate information in the response as possible so the sender knows what is happening and can act accordingly. Transparency in the workflow is essential to enable senders and receivers to work together to provide the best patient experience possible. 

### HTTP Response Headers
Responses to requests in the BaRS standard need not include anymore than Headers required by the HTTP protocol and the Transaction Integrity Headers listed above. Senders should not expect or require anymore than this in a synchronous HTTP response.

For secure usage of HTTP headers, guidance can be found in the OWASP Secure headers project regarding the [security headers](https://owasp.org/www-project-secure-headers/#div-headers) and [prevention of information disclosure](https://owasp.org/www-project-secure-headers/#div-bestpractices) which can be leveraged.


## Processing requests

For GET requests (reads) the receiver honours what is being asked for by generating and synchronously sending a response, for example the server Capability Statement on a GET /metadata request. Any failure during processing must initiate an error response back to the Sender. 

The $process-message endpoint on the implemented API supports a mix of RESTful and Messaging exchanges, as required by BaRS. The main benefit of introducing messaging is to allow a sender to package up the information a receiver needs, to process a particular request, but letting them handle it as necessitated by their system, rather than a sender having to make numerous requests to REST endpoints to perform the same action. 

When a request is received against the $process-message endpoint, the MessageHeader resource must be examined to determine what process the sender is expecting the receiver to perform. There are three key elements to determine this - 

- Event - primary function being asked to perform, for example: booking-request or servicerequest-request 
- Reason - operation, for example:. New or Update 
- Focus - the key resource in the bundle, to be read first to make sense of other related resources

The receiver interprets the request, engages the processing and synchronously feeds back a response. 

### Responses

In the BaRS workflows responses are an important step and likely to become more so as use cases offer up increasingly complex requirements, for example: negotiated referrals.

### Reversing roles

When responding the sender and receiver roles are reversed. Here you are essentially building a sender, and still need to implement a $process-message endpoint. Similarly, a receiver needs the ability to send the response to the BaRS API and will need to [register with our platform](https://digital.nhs.uk/developer/guides-and-documentation/security-and-authorisation/application-restricted-restful-apis-signed-jwt-authentication). 

### Asynchronous workflow

The FHIR $process-message function supports 'async' parameter but BaRS does not employ this, all $process-message requests are synchronous.

However, BaRS does support request-response loops which are asynchronous. An example of this is the Safeguarding DNA response workflow; the sender (NHS 111 Telephony service) sends a referral with a safeguarding concern flag to an Emergency Department, the patient subsequently doesn't attend (DNAs). The Emergency Department receiver is now responsible for sending a response back to the original sender (the NHS 111 Telephony service) to inform them of the DNA.

<hr>