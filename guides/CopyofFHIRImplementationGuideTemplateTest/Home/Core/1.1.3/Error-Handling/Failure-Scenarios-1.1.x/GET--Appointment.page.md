## GET /Appointment
This section defines the failure scenarios for GET /Appointment. There are two ways to call this endpoint. Either with a query parameter, or a path parameter. This section covers both of those methods.

### Rules

**GET /Appointment**
* query parameter identifier patient.identifier MUST be included.
* query parameter identifier patient.identifier MUST be a system:value. example: https://fhir.nhs.uk/Id/nhs-number|4857773456

**GET /Appointment/{id}**
* id in path MUST be a valid GUID/UUID

### Interactions

  ![BaRS FHIR API end-to-end process](https://raw.githubusercontent.com/NHSDigital/booking-and-referral-media/master/src/images/FailureScenarios/Appt-FailureScenarios-1.0.0.svg)
  
### Errors by parameter
**path id in GET /Appointment{id}**

| HTTP Status Code | HTTP Error Code  | issue Code | Scenario                                                                                      | Source   |
|------------------|------------------|------------|-----------------------------------------------------------------------------------------------|----------|
| 400              | SEND_BAD_REQUEST | required   | The parameter value was not included in the request.                                          | API      |
| 400              | REC_BAD_REQUEST  | required   | The parameter value was not included in the request.                                          | Receiver |
| 400              | REC_BAD_REQUEST  | value      | The identifier was in the incorrect format.                                                   | Receiver |
| 404              | REC_NOT_FOUND    | not-found  | The resource requested was not found.                                                         | Receiver |

**patient:identifier parameter identifier in GET /Appointment**

| HTTP Status Code | HTTP Error Code  | issue Code | Scenario                                                                                      | Source   |
|------------------|------------------|------------|-----------------------------------------------------------------------------------------------|----------|
| 400              | SEND_BAD_REQUEST | required   | The parameter value was not included in the request.                                          | API      |
| 400              | REC_BAD_REQUEST  | required   | The parameter value was not included in the request.                                          | Receiver |
| 400              | SEND_BAD_REQUEST | value      | the identifier was in the incorrect format.                                                   | API      |
| 400              | REC_BAD_REQUEST  | value      | the identifier was in the incorrect format.                                                   | Receiver |
