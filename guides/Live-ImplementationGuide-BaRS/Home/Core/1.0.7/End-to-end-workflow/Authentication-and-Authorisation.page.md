---
topic: core-EndToEndWorkflow-Auth-1.0.7
---

## {{page-title}}

| Header                       | Requirement                                              | Description                                                                                                                                                                                                                         | Value                                                       |
|------------------------------|----------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------|
| Authorisation                | Required by the sender and not forwarded to the receiver | Will contain a token obtained from the relevant OAuth endpoint for the BaRS API being called. This token facilitates authentication with the API.                                                                                   | String representing a token                                 |
| NHSD-End-User- Organisation  | Optional for the sender and forwarded to the receiver    | For authorisation purposes this header contains information about the organisation making the request. Can be used by the receiver to impose access control limitations and should be retained for auditing purposes.               | Base64 encoded object based on a FHIR Organization resource |
| NHSD-Requesting-Practitioner | Optional for the sender and forwarded to the receiver    | For authorisation purposes this header contains information about the healthcare professional making the request. Can be used by the receiver to impose access control limitations and should be retained for auditing purposes.    | Base64 encoded object based on a FHIR PractitionerRole resource |
| NHSD-Requesting-Software     | Optional for the sender and forwarded to the receiver    | For authorisation purposes this header contains information about the  application making the request. This can be used by the receiver to impose access control limitations and should be retained for auditing purposes.          | Base64 encoded object based on a FHIR Device resource       |

<hr>
<br>