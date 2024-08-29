---
topic: Core-TransactionalIntegrity-Retry-1.1.3
---

## Retry scenario

Should a request fail for any reason and the sender not receive a response (in any of the above scenarios) the sender is to retry the request, retaining the same X-Request-ID and X-Correlation-ID as the initial attempt. This allows the receiver to identify whether it has already processed this message or not.

![BaRS FHIR API end-to-end process](https://raw.githubusercontent.com/NHSDigital/booking-and-referral-media/master/src/images/TransactionIntegrity/Retry-Scenario-1.0.0.svg)


This satisfies the need to be able to handle transaction integrity, and for the most part auditing/logging. There are two more scenarios that need to be clarified:

- onwards referrals
- sending a booking and referral

The proposal is to retain the X-Correlation-ID for two separate and distinct messages concerning the same encounter or case.

<br>
<hr>