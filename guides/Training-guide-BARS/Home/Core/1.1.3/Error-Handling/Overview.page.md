---
topic: core-ErrorHandling-Overview-1.1.3
---

### Overview

Error codes (HTTP Response codes) can be caused by any of the three parties involved in a transaction using the Booking and Referral API. Error codes will be accompanied by a OperationOutcome FHIR resource where possible.  Error codes and their relative operation outcome codes are meant for developer use only - they should not be presented to end-users. Instead, sending applications should interpret the two codes and provide user-friendly resolution steps on failure. Sender and receiver systems should record the detailed error codes in local logs in order to support service incident investigation. There are scenarios where an operation outcome may not be applicable or available. A HTTP Response code should always be returned.

Operation Outcome Codes are prefixed with an indicator of the source of the error help identify where a problem may be.

The following table provides a high-level overview of each stage in the booking and referral process from the perspective of a sending application.

| Interaction                              | Error Handling Overview                                                                                                                                                                                                                                                                                                                                                         | Operation Outcome Prefix |
|------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------|
| Sender querying a Service Discovery tool | As an existing solution, the DOS APIs return a number of significant errors specific to the actual API failing. These are all self-contained in that process. These are documented in a link below and will not affect the ongoing activity unless the data returned in the query is erroneous and then cause the next stages of the process to either fail or not be possible. | N/A                      |
| Sender interactions with the BaRS API    | Interactions with the BaRS API may fail due to, but not limited to, the following reasons: The service being unavailable to the sender, the Sender being unauthenticated, the Sender reaching or exceeding a rate limit, or badly formed requests being sent.                                                                                                                   | SEND                     |
| BaRS Service internal interactions       | Depending on the operation requested, internal interactions may fail within the proxy due to non-existent resources, service failures or data related issues within the Senders payload.                                                                                                                                                                                        | PROXY                    |
| BaRS interaction with the Receiver       | In the event BaRS successfully proxies a request through to a Receiver, the Receiver may still respond with an error due to authentication, authorization or data related issues within the Senders payload, assuming the endpoint is available.                                                                                                                                | REC                      |

<br>
<hr>