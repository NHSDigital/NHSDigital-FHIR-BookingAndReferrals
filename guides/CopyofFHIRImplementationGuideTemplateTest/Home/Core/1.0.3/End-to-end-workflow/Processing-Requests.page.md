## {{page-title}}

For GET requests (reads) the receiver honours what is being asked for by generating and synchronously sending a response, for example the server Capability Statement on a GET /metadata request. Any failure during processing must initiate an error response back to the Sender. 

The $process-message endpoint on the implemented API supports a mix of RESTful and Messaging exchanges, as required by BaRS. The main benefit of introducing messaging is to allow a sender to package up the information a receiver needs, to process a particular request, but letting them handle it as necessitated by their system, rather than a sender having to make numerous requests to REST endpoints to perform the same action. 

When a request is received against the $process-message endpoint, the MessageHeader resource must be examined to determine what process the sender is expecting the receiver to perform. There are three key elements to determine this - 

- Event - primary function being asked to perform, for example: booking-request or servicerequest-request 
- Reason - operation, for example:. New or Update 
- Focus - the key resource in the bundle, to be read first to make sense of other related resources

The receiver interprets the request, engages the processing and synchronously feeds back a response.

Please see the {{pagelink:Core-StandardPattern-1.0.3, text: Standard Patterns}} for generic guidance for processing messages.

<br>