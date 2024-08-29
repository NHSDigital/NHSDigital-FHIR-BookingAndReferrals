## GET /MessageDefinition
Message definition includes only one additional parameter and therefore there are less scenarios to cover.

### Rules
* The context query parameter must be present.
    * For current use cases this will always match the value in the NHSD-Target-Identifier header. This could could not always be the case in future.

### Interactions

  ![BaRS FHIR API end-to-end process](https://raw.githubusercontent.com/NHSDigital/booking-and-referral-media/master/src/images/FailureScenarios/MessageDefinition-FailureScenarios-1.0.0.svg)
  
### Errors by parameter

**context**

| HTTP Status Code | HTTP Error Code  | issue Code | Scenario                                         | Source   |
|------------------|------------------|------------|--------------------------------------------------|----------|
| 400              | SEND_BAD_REQUEST | required   | no context parameter was given.                  | API      |
| 400              | REC_BAD_REQUEST  | required   | no context parameter was given.                  | Receiver |
| 400              | REC_BAD_REQUEST  | invalid    | the context parameter value was invalid (format) | Receiver |
| 400              | REC_BAD_REQUEST  | value      | the context parameter value was invalid (format) | Receiver |
| 404              | REC_NOT_FOUND    | not-found  | the context parameter given returned no results. | Receiver |

### Standard errors
| HTTP Status Code | HTTP Error Code         | issue Code | Scenario                                                                                                                                                                                   | Source                  |
|------------------|-------------------------|------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------|
| 400              | REC_BAD_REQUEST         | invalid    | Although this should be caught at the proxy/API, should a request be received with no X-Request-Id or X-Correlation-Id be received this check should be in place. (BaRS without the Proxy) | Receiver                |
| 400              | REC_BAD_REQUEST         | value      | As above, but the value is not a GUID/UUID.                                                                                                                                                     | Receiver                |
| 401              | REC_UNAUTHORIZED        | security   | Access Control issue.                                                                                                                                                                      | Receiver                |
| 403              | REC_FORBIDDEN           | forbidden  | TLS-MA failure.                                                                                                                                                                            | Receiver                |
| 403              | REC_FORBIDDEN           | security   | TLS-MA failure.                                                                                                                                                                            | Receiver                |
| 500              | REC_SERVER_ERROR        | exception  | an unhandled exception has been encountered.                                                                                                                                               | Receiver / API Injected |
| 503              | REC_SERVICE_UNAVAILABLE | transient  | The service(s) is unavailable but is able to respond as such, otherwise injected.                                                                                                          | Receiver / API Injected |
