---
topic: Core-TransactionalIntegrity-Receiver-1.1.3
---

## Receiver responsibilities

- return the  X-Request-ID and X-Correlation-ID in responses at ALL times, where possible
- reject any message with no X-Request-ID and X-Correlation-ID, without exception with REC_BAD_REQUEST (400)
- in the event that a duplicate message that has already been correctly processed is received, return a response with REC_CONFLICT (409) and an operationOutcome.issue.code of "duplicate"
- this combination of codes can only be used in a duplicate message scenario

<br>
<hr>