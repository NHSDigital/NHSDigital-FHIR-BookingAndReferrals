---
topic: core-ErrorHandling-RecResp-1.1.3
---

### Receiver responsibilities

- Receiving APIs should adhere to the HTTP Response code and Operational Outcome code paradigm described above in the event that an error response needs to be returned
- The sender should be able to ascertain what went wrong and why in the event of an error
- Receiving endpoints should use the REC prefixed Operation Outcome codes and provide clear and concise diagnostics texts
- There should be no need to omit or use a different prefix when responding to requests
- There will be times where it is not possible to generate a response in the above format
- In the event this occurs, a relevant HTTP response code should be the minimum
- Log errors locally for incident investigation by IT support staff
- If the request is problematic, this should be logged specifically as a sender system issue
- Details of the sender system should be logged to support investigation
- As a minimum, the Operation Outcome must include:
	- The HTTP Response code
	- The Operation Outcome code
	- Clear and concise diagnostics information

<br>
<hr>