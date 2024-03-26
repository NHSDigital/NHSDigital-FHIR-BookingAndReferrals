## {{page-title}}

| Header           | Requirement                                                       | Description                                                               | Value  |
|------------------|-------------------------------------------------------------------|---------------------------------------------------------------------------|--------|
| X-Request-ID     | Required for sending of any request and forwarded to the receiver | Will facilitate transactional integrity and the ability to audit messages | UUID   |
| X-Correlation-Id | Required for sending of any request and forwarded to the receiver | Will facilitate transactional integrity and the ability to audit messages | UUID   |

We expect receivers to use and store the header values in the following ways:

- to ensure the message maintains transactional integrity and hasn't been received previously 
- to check who has sent the request and apply access control if desired
- to ensure all interactions are auditable

If at any point the request fails, the receiver must send an appropriate error response (see Error handling) back to the sender to inform them why the request cannot be fulfilled. It is important to return as accurate information in the response as possible so the sender knows what is happening and can act accordingly. Transparency in the workflow is essential to enable senders and receivers to work together to provide the best patient experience possible. 

<hr>
<br>