 # {{page-title}}

BaRS uses [FHIR](https://digital.nhs.uk/services/fhir-uk-core) to achieve interoperability between healthcare IT systems. This section explains how BaRS makes use of some key FHIR concepts which need to be understood by developers implementing the standard. 

### Frameworks

A mix of data exchange frameworks are employed by BaRS to support different workflows. 

### REST 

FHIR is often associated with REST (REpresentational State Transfer) as a primary method of exchange. BaRS uses REST for many of the benefits it offers - 

- allows independent modular development of client and server APIs (they don't need to know about each other before exchanges)
- easy to integrate because of common agreed standards
- scalability in developing and performance 

In BaRS, simple CRUD operations on single resources is used for discrete atomic functions, such as retrieving a known booking or referral entity. 

### FHIR Operations framework 

Performing the required steps in workflow using simple CRUD operations on single resources can be complex and relies on prior knowledge or dictates explicit rules around workflow in any given system, for example: a patient must exist before a service request can be made. In order to support complex workflows that utilise composites of resources, simple CRUD operations on sinlge resources would breach some core principles of ReST (e.g. inabililty to maintain stateless communication for example). Therefore BaRS utilises the FHIR operations framework which:

- offers a degree of autonomy to the receiver of the communication in how they process for their system
- is designed to support events, triggering activity between systems, supporting the response workflow requirements identified by many of the BaRS use cases, for example:  999 to CAS Validation Request/Response.

### $process-message 

This specific FHIR operation enables the exchange of complex composites whilst maintaining the principles of REST. The $process-message endpoint will be called at various stages in any of the workflows outlined to fulfil requests such as:

- 'create a booking'
- 'process a referral for validation' 
- 'validation outcome response'

The endpoint receives only POST requests of bundle type 'message', with the required MessageHeader resource dictating how to process and what is deemed the 'focus' (key Resource) of the request. The sender packages up this content, POSTs to the receiver and lets them decide how to consume and process the bundle. 

You must implement a $process-message endpoint to be compliant with BaRS because it is used for initial requests (booking, service request etc.) but also for responses (validation outcome response etc.). 

### Bundle

The use of the FHIR bundle in BaRS primarily supports the use of $process-message. It is also used as follows:

- When $process-message is initiated, a sender packages up numerous FHIR resources (MessageHeader, Patient, ServiceRequest etc.), the bundle will include everything needed by a receiver to process the request being made.
- The $process-message endpoint is capable of receiving different types of request. The sender indicates the the action required by specifying in the MessageHeader resource, for example: booking or servicerequest, the operation, whether it be 'new' or 'update' and central FHIR resource from which to make sense of the bundle, the 'focus'.
- A bundle type of 'searchset' is also used in BaRS when a receiver responds to a senders request for available slots, in the booking workflow. A receiver responds by bundling FHIR resources (HealthcareService, Schedule, Slot(s) etc.) related to particular HealthcareService which a sender will unpack and process to display service availability to a user.

<hr>