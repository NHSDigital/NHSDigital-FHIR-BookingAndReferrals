---
topic: Core-TransactionalIntegrity-1.0.3
---

## {{page-title}}

Transactional integrity is employed to ensure data integrity is maintained between two parties. It helps ensure that the success or failure of a message is known and can be confirmed. 

There are two existing header items for requests currently available to allow BaRS to meet transactional integrity requirements. They are listed below with their intended uses. The [BaRS API specification](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_0_0) contains example values for these entries.

| Header           | Requirement  | Description                                                                                                                                   | Value                      |
|------------------|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------|----------------------------|
| X-Correlation-ID | Required     | A globally unique identifier for the request that can be used to track related transactions across multiple systems.                          | string representing a GUID |
| X-Request-ID     | Required     | A globally unique identifier for the request, used to de-duplicate repeated requests and to trace the request for support purposes if needed. | string representing a GUID |

Transactional integrity is based on guidance in the [FHIR standard](https://www.hl7.org/fhir/http.html#custom). The header items are used as outlined below:

- the sender will generate both IDs at the beginning of a request for a message.
- the receiver will respond to this initial message, echoing back both IDs. The receiving server does not need to generate a new ID.
- any feedback requests from receiver to the initial sender shall use a new X-Request-ID but retain the X-Correlation-ID. This will be as a new message of the same conversation.
- any subsequent updates from the sender to the receiver shall use a X-Request-ID but will retain the original X-Correlation-ID. This will be as a new message of the same conversation.
- any onward referrals of a message will use a new X-Request-ID but retain the X-Correlation-ID
- a receiver of any message will not accept two messages with the same request and X-Correlation-IDs

<br>
<hr>