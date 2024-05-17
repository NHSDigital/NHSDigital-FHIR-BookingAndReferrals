## GET /Slots
Get /Slots has added complexity compared to previous endpoints in this section. With a myriad of available and required parameters there is a potential for many scenarios.

### Rules
* Schedule:actor:HealthcareService - Must be included.
  * For current use cases this will likely match the value in the NHSD-Target-Identifier header. This may not always be the case in future.
* _include - There is a minimum of the following 2 _includes required for current Applications.
  * Slot:schedule
  * Schedule:actor:HealthcareService
* start - The start parameter must be used twice, and adds the need for handling problematic requests with its use (too wide a time frame, as an example).
  * Must use the [FHIR instant](https://www.hl7.org/fhir/datatypes.html#primitive) format which includes and offset.
  * Must be UTC
  * Must have a greater than and a less than.
* status - The status parameter must be used.
  * multiple statuses must be comma separated.
  * FOT allows free or busy.

### Interaction  

  ![BaRS FHIR API end-to-end process](https://raw.githubusercontent.com/NHSDigital/booking-and-referral-media/master/src/images/FailureScenarios/Slot-FailureScenarios-1.0.0.svg)
  
### Errors by parameter
**Schedule:actor:HealthcareService**

| HTTP Status Code | HTTP Error Code                     | issue Code        | Scenario                                                                                                    | Source           |
|------------------|-------------------------------------|-------------------|-------------------------------------------------------------------------------------------------------------|------------------|
| 400              | SEND_BAD_REQUEST / REC_BAD_REQUEST? | required          | The parameter value was not included in the request. (This parameter is not currently marked as required. ) | API and Receiver |
| 400              | REC_BAD_REQUEST                     | value / invariant | The parameter value was incorrect or wrong.                                                                 | Receiver         |
| 401              | REC_UNAUTHORIZED                    | forbidden         | The Sending organisation/ software/ practitioner Role does is not allowed to access this information, evaluated in their corresponding Access Control headers.       | Receiver         |
| 404              | REC_NOT_FOUND                       | not-found         | This service does not exist.                                                                                | Receiver         |
 
**_include**

| HTTP Status Code | HTTP Error Code  | issue Code | Scenario                                                                                                    | Source           |
|------------------|------------------|------------|-------------------------------------------------------------------------------------------------------------|------------------|
| 400              | REC_BAD_REQUEST  | required   | the minimum required includes are not present.                                                              | API and Receiver |
| 401              | REC_UNAUTHORIZED | forbidden  | The Sending organisation/ software/ practitioner Role does is not allowed to access this information, evaluated in their corresponding Access Control headers. | Receiver         |

**start**

| HTTP Status Code | HTTP Error Code                    | issue Code | Scenario                                                                                              | Source           |
|------------------|------------------------------------|------------|-------------------------------------------------------------------------------------------------------|------------------|
| 400              | SEND_BAD_REQUEST / REC_BAD_REQUEST | required   | Date range was not present.                                                                           | API and Receiver |
| 400              | SEND_BAD_REQUEST / REC_BAD_REQUEST | value      | DateTimes in the requested start time range requested was invalid.                                    | API and Receiver |
| 401              | REC_UNAUTHORIZED                   | forbidden  | The Sending organisation/ software/ practitioner Role does is not allowed to access this information, evaluated in their corresponding Access Control headers. | Receiver         |
| 422              | REC_UNPROCESSABLE_ENTITY           | too-costly | The start time range requested is too wide.                                                           | Receiver         |


**status**

| HTTP Status Code | HTTP Error Code                    | issue Code | Scenario                           | Source           |
|------------------|------------------------------------|------------|------------------------------------|------------------|
| 400              | SEND_BAD_REQUEST / REC_BAD_REQUEST | required   | status not present.                | API and Receiver |
| 400              | SEND_BAD_REQUEST / REC_BAD_REQUEST | value      | status value requested is invalid. | API and Receiver |

**Common Failures**

| HTTP Status Code | HTTP Error Code         | issue Code | Scenario                                                                                                                                                          | Source                  |
|------------------|-------------------------|------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------|
| 400              | REC_BAD_REQUEST         | invalid    | Although this should be caught at the proxy/API, should a request be received with no X-Request-Id or X-Correlation-Id be received this check should be in place. | Receiver                |
| 400              | REC_BAD_REQUEST         | value      | As above, but the value is not a GUID/UUID.                                                                                                                            | Receiver                |
| 401              | REC_UNAUTHORIZED        | security   | Access Control issue.                                                                                                                                             | Receiver                |
| 403              | REC_FORBIDDEN           | forbidden  | TLS-MA failure.                                                                                                                                                   | Receiver                |
| 403              | REC_FORBIDDEN           | security   | TLS-MA failure.                                                                                                                                                   | Receiver                |
| 500              | REC_SERVER_ERROR        | exception  | an unhandled exception has been encountered.                                                                                                                      | Receiver / API Injected |
| 503              | REC_SERVICE_UNAVAILABLE | transient  | The service is unavailable but is able to respond as such.                                                                                                        | Receiver / API Injected |
