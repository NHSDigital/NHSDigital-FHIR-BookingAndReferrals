---
topic: core-ErrorHandling-Examples-1.1.3
---

### Example errors

The table below contains some further examples of error codes, their associated Operation Outcomes codes and and potential diagnostics texts.

| HTTP Code | Code Value            | Description                                                                                                 | Example diagnostics text                                                                                                                    |
|-----------|-----------------------|-------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------|
| 400       | SEND_BAD_REQUEST      | The API was unable to process the request.                                                                  | "The API was unable to process the request: <further diagnostics information, error message/error text>"                                    |
|           | REC_BAD_REQUEST       | The Receiver has responded stating the message was malformed.                                               | "<Receiver Identifier (ODS)> was unable to process the request: <further diagnostics information, error message/error text>"                |
|           | PROXY_BAD_REQUEST     | Though Unlikely, BaRS, having accepted the message; has received a 400 response from an internal component. | "BaRS was unable to process the request: <further diagnostics information, error message/error text>"                                       |
| 404       | PROXY_NOT_FOUND       | The resource was not found within BaRS.                                                                     | "The resource was not found within BaRS: <further diagnostics information, error message/error text>"                                       |
|           | REC_NOT_FOUND         | The resource was not found at the Receiver.                                                                 | "<Receiver Identifier (ODS)> encountered a conflict: <further diagnostics information, error message/error text>"                           |
| 409       | REC_CONFLICT          | Example: Sender is trying to Book an appointment in a slot that doesn't allow booking.                      | "<Receiver Identifier (ODS)> encountered a conflict: <further diagnostics information, error message/error text>"                           |
| 501       | SEND_NOT_IMPLEMENTED  | The Request was not recognized.                                                                             | "The Request was not recognized by the API: <further diagnostics information, error message/error text>"                                    |
|           | REC_NOT_IMPLEMENTED   | The Receiver did not recognize the request.                                                                 | "The Request was not recognised by the Receiver - <Receiver identifier (ODS)>: <further diagnostics information, error message/error text>" |
|           | PROXY_NOT_IMPLEMENTED | BaRS did not recognize the request.                                                                         | "This Request was not recognized by the proxy: <further diagnostics information, error message/error text>"                                 |

<br>
<hr>