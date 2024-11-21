---
topic: core-EndToEndWorkflow-Processing-1.2.1
---


## {{page-title}}

For GET requests (reads) the Receiver honours what is being asked for by generating and synchronously sending a response, for example the server Capability Statement on a GET /metadata request. Any failure during processing must initiate an error response back to the Sender. 

The $process-message endpoint on the implemented API supports a mix of RESTful and Messaging exchanges, as required by BaRS. The main benefit of introducing messaging is to allow a Sender to package up the information a Receiver needs, to process a particular request, but letting them handle it as necessitated by their system, rather than a Sender having to make numerous requests to REST endpoints to perform the same action. 

When a request is received against the $process-message endpoint, the MessageHeader resource must be examined to determine what process the Sender is expecting the Receiver to perform. There are three key elements to determine this - 

- .eventCoding - primary function being asked to perform, for example: booking-request or servicerequest-request 
- .reason - operation, for example:. New or Update 
- .focus - the key resource in the bundle, to be read first to make sense of other related resources

The Receiver interprets the request, engages the processing and synchronously feeds back a response.

When processing the body (the FHIR bundle or payload) of the request, the Receiver can implement business logic, determining the type of payload and whether a request is valid or not, by using the guidance under the payload sections of each Application. This guidance stiplates the business requirement of each element of the payload, allowing a Receiver to determine elements which are mandated, required, optional or forbidden. The 'Necessity' column, of the tables within each Application payload section, indicates these buisness level requirements and aligns with defintions under [RFC 2119](https://datatracker.ietf.org/doc/html/rfc2119).

Please see the {{pagelink:Core-StandardPattern-1.2.1, text: Standard Patterns}} for generic guidance for processing messages.

<br>