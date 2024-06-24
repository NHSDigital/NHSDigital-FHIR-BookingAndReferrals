---
topic: Core-ErrorHandling-MessageRouting-1.1.3
---

## Endpoint Catalogue - Message routing.

<div id="message_routing"></div>

Below is a diagram of error locations coupled with scenarios with regards to the routing of messages by the proxy using the Endpoint Catalogue. The below diagram is generic and not specific to any particular API endpoint. Most requests will be subject to the errors that can be encountered during message routing.

  ![BaRS FHIR API end-to-end process](https://raw.githubusercontent.com/NHSDigital/booking-and-referral-media/master/src/images/FailureScenarios/EndpointCatalogue-FailureScenarios-1.0.0.svg)

### SEND at the API
The SEND prefix indicates an issue caught before any internal routing or processing occurs, it communicates a problem with the format of the request, not adhering to the API Spec as an example.

These scenarios can be found in other areas however if more required headers are added for endpoints this may be expanded. 

| HTTP Status Code | HTTP Error Code                         | issue Code | Scenario                                                                                                                                                  | Source |
|------------------|-----------------------------------------|------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|--------|
| 400              | SEND_BAD_REQUEST                        | required   | The X-Request-Id or the X-Correlation-Id was not included or the NHSD-Target-Identifier was not included (depending on the endpoint being called).        | API    |
| 401              | SEND_UNAUTHORIZED                       | security   | The user or system was not able to be authenticated, either the access token was invalid, or not provided.                                                | API    |
| 401              | SEND_UNAUTHORIZED                       | unknown    | No Access token was provided.                                                                                                                             | API    |
| 403              | SEND_FORBIDDEN                          | forbidden  | The access token was provided, but BaRS is not enabled.                                                                                                   | API    |
| 404              | PROXY_NOT_FOUND / NOT_FOUND             | not-found  | Endpoint on the API does not exist. This would be a Proxy or non-prefixed response. there is no SEND code for 404 in the value set.                       | API    |
| 500              | PROXY_SERVER_ERROR / SERVER_ ERROR      | exception  | Unexpected error, would expect this to happen internally so this is likely never going to be needed for a SEND and thus unprefixed or PROXY is used here. | API    |
| 503              | PROXY_UNAVAILABLE / SERVICE_UNAVAILABLE | transient  | unlikely to get a OperationOutcome here.                                                                                                                  | API    |

### PROXY/NONE within the BaRS proxy


| HTTP Status Code | HTTP Error Code                         | issue Code       | Scenario                                                                                                                                           | Source |
|------------------|-----------------------------------------|------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|--------|
| 400              | PROXY_BAD_REQUEST / BAD_REQUEST         | invalid          | The X-Request-Id or the X-Correlation-Id was invalid.                                                                                              | API    |
| 400              | PROXY_BAD_REQUEST / BAD_REQUEST         | invalid          | When Base-64 decoding of the NHSD-Target-Identifier header fails.                                                                                  | API    |
| 400              | PROXY_BAD_REQUEST / BAD_REQUEST         | structure        | The NHSD-Target-Identifier header doesn't adhere to the schema                                                                                     | API    |
| 400              | PROXY_BAD_REQUEST / BAD_REQUEST         | required         | A required item is missing. depending on the request/scenario this may be caught by the SEND details above.                                        | API    |
| 400              | PROXY_BAD_REQUEST / BAD_REQUEST         | structure        | A structural issue in the content such as wrong namespace, unable to parse the content completely - for example the Target identifier is malformed.| API    |
| 404              | PROXY_NOT_FOUND / NOT_FOUND             | not-found        | The resource requested does not exist. For example; the target endpoint does not exist in the Endpoint Catalogue.                                  | API    |
| 404              | PROXY_NOT_FOUND / NOT_FOUND             | multiple-matches | The Target Identifier found two endpoints, this would be an issue with the management of the Endpoint catalogue.                                   | API    |
| 500              | PROXY_SERVER_ERROR / SERVER_ERROR       | exception        | A sub-service encountered an unhandled exception.                                                                                                  | API    |
| 503              | PROXY_UNAVAILABLE / SERVICE_UNAVAILABLE | transient        | A sub-service was unavailable.                                                                                                                     | API    |

### REC injected at the proxy
When a failure response is received when attempting to forward the request to the desired receiver but no OperationOutcome is included during a failure scenario. For example, a Timeout.

| HTTP Status Code | HTTP Error Code         | issue Code | Scenario                                                                                                                                                            | Source                     |
|------------------|-------------------------|------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------|
| 408              | REC_TIMEOUT             | timeout    | The connection to the Receiver timed out.                                                                                                                           | Receiver/ Injected at API  |
| 500              | REC_SERVER_ERROR        | exception  | Generic should a 500 response be received but no operation outcome included.                                                                                        | Receiver / Injected at API |
| 503              | REC_SERVICE_UNAVAILABLE | transient  | The response from the receiver was a 503, with no detail. Also useful if there is a connection failure such as the endpoint not being found, or failing to resolve. | Receiver / Injected at API |

### REC at the receiver. 
Failure responses generated by the receiver.

| HTTP Status Code | HTTP Error Code  | issue Code | Scenario                                                     | Source                     |
|------------------|------------------|------------|--------------------------------------------------------------|----------------------------|
| 401              | REC_UNAUTHORIZED | security   | Access Control                                               | Receiver                   |
| 403              | REC_FORBIDDEN    | forbidden  | TLS-MA failure.                                              | Receiver                   |
| 403              | REC_FORBIDDEN    | security   | TLS-MA failure.                                              | Receiver                   |
| 500              | REC_SERVER_ERROR | too costly | The request was deemed to costly to process by the receiver. | Receiver                   |
| 500              | REC_SERVER_ERROR | exception  | unhandled exception.                                         | Receiver / Injected at API |
| 500              | REC_SERVER_ERROR | no-store   | internal data storage issue.                                 | Receiver / Injected at API |

