---
topic: Core-TransactionalIntegrity-Sender-1.0.3
---

## Sender responsibilities

The frequency of retries and the duration of a retry period depends on the scenario and should not disrupt workflow. Exponential backoff is considered best practice however it is at the discretion of the sender to define how many times a retry is attempted.

- retry in the event X-Request-ID and X-Correlation-ID is not in the response
- retry in the event no OperationOutcome is in the body of the response
- retry when an OperationOutcome from a receiver contains one of the following values and response codes:
    - REC_TIMEOUT (408)
    - REC_TOO_MANY_REQUESTS (429)
    - REC_UNAVAILABLE (503)
-retry when an OperationOutcome from BaRS itself contains one of the following:
    - PROXY_TIMEOUT / TIMEOUT (504 indicating 408 internally)
    - PROXY_TOO_MANY_REQUESTS / TOO_MANY_REQUESTS (500 indicating a 408 internally)
    - PROXY_UNAVAILABLE  / UNAVAILABLE (503)
- retry when an OperationOutcome from the BaRS API contains one of the following:
    - SEND_TOO_MANY_REQUESTS (429)
    - SEND_FORBIDDEN (403), on the assumption the access token issue is resolved
- it is then at the senders discretion as to whether they update other properties of the message accordingly
- do not retry a request again if a response with the following attributes is received, this indicates the message was successfully sent
    - REC_CONFLICT (409)
    - an operationOutcome.issue.code of "duplicate"

Any intermediary network device responding 'on behalf or in lieu' of the API or the receiver is not likely to respond with an OperationalOutcome or the required X-Request-ID and X-Correlation-ID. Any response not having either one of these properties can be safely deemed a communications failure, a temporary interruption to connectivity or could potentially indicate a service outage. Any of these scenarios could, but not always, warrant an retry. This would be at the discretion of the suppliers however these failed interactions should be logged with as much detail as possible. Errors outside of the HTTP standard should also be logged locally with as much detail as possible, for example; Transport-Layer error messages.

<br>
<hr>