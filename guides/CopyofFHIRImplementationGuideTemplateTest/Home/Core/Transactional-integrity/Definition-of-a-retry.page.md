## Definition of a retry

In this context a retry is an attempt to send the same message, without any changes following a failure. This means:

- the Message body is the same
- the X-Request-ID and X-Correlation-ID are unchanged
- no other header items have changed. (with the potential exemption of the Access Token)

<br>
<hr>