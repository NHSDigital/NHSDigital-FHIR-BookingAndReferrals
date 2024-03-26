## Bundle

The use of the FHIR bundle in BaRS primarily supports the use of $process-message. It is also used as follows:

- When $process-message is initiated, a sender packages up numerous FHIR resources (MessageHeader, Patient, ServiceRequest etc.), the bundle will include everything needed by a receiver to process the request being made.
- The $process-message endpoint is capable of receiving different types of request. The sender indicates the the action required by specifying in the MessageHeader resource, for example: booking or servicerequest, the operation, whether it be 'new' or 'update' and central FHIR resource from which to make sense of the bundle, the 'focus'.
- A bundle type of 'searchset' is also used in BaRS when a receiver responds to a senders request for available slots, in the booking workflow. A receiver responds by bundling FHIR resources (HealthcareService, Schedule, Slot(s) etc.) related to particular HealthcareService which a sender will unpack and process to display service availability to a user.

<br>
<hr>