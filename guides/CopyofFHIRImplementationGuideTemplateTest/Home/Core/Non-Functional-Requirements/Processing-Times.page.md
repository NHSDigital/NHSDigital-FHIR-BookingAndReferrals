## {{page-title}}

The following Processing time SLAs describe the need for APIs to respond to a request within an acceptable time frame. This time frame should be measured from when a request is received and does not include the transport time.
These times are guide for average response time.

| item | Requirement.                                                                                                                                                   |
|------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1    | 90% of requests SHOULD take less than 2100ms to process. (Allowing for response time depending on measurement point). $process-message independently measured. |
| 2    | All requests MUST take less than 5000ms to process.                                                                                                            |
| 3    | Any requests not processed within 5000ms should be timed out with "408 - REC_TIMEOUT - timeout"                                                    