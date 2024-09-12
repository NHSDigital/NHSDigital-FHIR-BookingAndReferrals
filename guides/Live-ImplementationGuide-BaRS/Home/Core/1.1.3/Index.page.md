---
topic: design-core-1.1.3
---

# BaRS Core 1.1.3

BaRS consists of BaRS Core that provides a core set of functionality and BaRS Applications that provide distinct functionality for each use case.

You will find here a set of documentation, specifications and services that describe and support all the fundamental components of the standard that are always the same for all use cases or care journeys. Examples include the underlying capabilities and patterns and transport layer elements such as security, authorisation and access control.

<details>
<summary>> <b class="barslink">Expand for full Core directory</b></summary>

&bull; {{pagelink:design-core-1.1.3 , text: Core 1.1.3}}</br>
&nbsp;&nbsp;&bull; {{pagelink:core-EndToEndWorkflow-1.1.3 , text:End to end workflow}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-EndToEndWorkflow-ServiceDiscovery-1.1.3 , text:Service Discovery}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-EndToEndWorkflow-BaRSAuth-1.1.3 , text:Authenticate with BaRS}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-EndToEndWorkflow-API-1.1.3 , text:BaRS FHIR API}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-EndToEndWorkflow-HTTPHeader-1.1.3 , text:HTTP Header}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-EndToEndWorkflow-Routing-1.1.3 , text:Routing}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-EndToEndWorkflow-Auth-1.1.3 , text:Authentication and Authorisation}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-EndToEndWorkflow-Transactional-Integrity-1.1.3 , text:Transactional Integrity}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-EndToEndWorkflow-HTTPResponseHeader-1.1.3 , text:HTTP Response Headers}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-EndToEndWorkflow-Processing-1.1.3 , text:Processing Requests}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-EndToEndWorkflow-Responses-1.1.3 , text:Responses}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-EndToEndWorkflow-ReversingRoles-1.1.3 , text:Reversing Roles}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-EndToEndWorkflow-AsyncWorkflow-1.1.3 , text:Asynchronous Workflow}}</br>
&nbsp;&nbsp;&bull; {{pagelink:core-FunctionalityRequirements-1.1.3 , text:Core Functionality Requirements.}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-FunctionalityRequirements-All-1.1.3 , text:All}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-FunctionalityRequirements-Caching-1.1.3 , text:Caching}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-FunctionalityRequirements-BookingSender-1.1.3 , text:Booking Sender}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-FunctionalityRequirements-BookingReceiver-1.1.3 , text:Booking Receiver}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-FunctionalityRequirements-ReferralSender-1.1.3 , text:Referral Sender}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-FunctionalityRequirements-ReferralReceiver-1.1.3 , text:Referral Receiver}}</br>
&nbsp;&nbsp;&bull; {{pagelink:core-FHIRUsage-1.1.3 , text:BaRS FHIR Usage}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-FHIRUsage-Framework-1.1.3 , text:Frameworks}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-FHIRUsage-REST-1.1.3 , text:REST}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-FHIRUsage-FHIR-Operations-1.1.3 , text:FHIR Operations}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-FHIRUsage-Process-Message-1.1.3 , text:$process-message}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-FHIRUsage-bundle-1.1.3 , text:Bundle}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-FHIRUsage-JourneyID-1.1.3 , text:Journey ID}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-FHIRUsage-Time-1.1.3 , text:How to handle times}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-FHIRUsage-LastUpdated-1.1.3 , text:LastUpdatedDate}}</br>
&nbsp;&nbsp;&bull; {{pagelink:core-Security-1.1.3 , text:Security and Authorisation}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-Security-Sender-1.1.3 , text:Sender}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-Security-Oauth-1.1.3 , text:OAuth Endpoints}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-Security-Receiver-1.1.3 , text:Receiver}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-Security-Auth-1.1.3 , text:Authorisation}}</br>
&nbsp;&nbsp;&bull; {{pagelink:core-ErrorHandling-1.1.3 , text:Error Handling}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-ErrorHandling-Overview-1.1.3 , text:Overview}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-ErrorHandling-IntS-1.1.3 , text:BaRS interactions(sending)}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-ErrorHandling-OpOut-1.1.3 , text:OperationOutcome Example}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-ErrorHandling-Diag-1.1.3 , text:Diagnostic Text}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-ErrorHandling-Examples-1.1.3 , text:Example Errors}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-ErrorHandling-SendResp-1.1.3 , text:Sender Responsibilities}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-ErrorHandling-IntR-1.1.3 , text:BaRs interactions(receiving)}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-ErrorHandling-RecResp-1.1.3 , text:Receiver responsibilities}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-failure_scenarios-1.1.3 , text:Failure Scenarios}}	 </br>
&nbsp;&nbsp;&bull; {{pagelink:Core-TransactionalIntegrity-1.1.3 , text:Transactional Integrity}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:Core-TransactionalIntegrity-Initial-1.1.3 , text:Initial Request}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:Core-TransactionalIntegrity-Update-1.1.3 , text:Sending an update}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:Core-TransactionalIntegrity-Feedback-1.1.3 , text:Feedback (response) requests}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:Core-TransactionalIntegrity-Retry-1.1.3 , text:Retry Scenario}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:Core-TransactionalIntegrity-Onward-1.1.3 , text:Onwards Referrals}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:Core-TransactionalIntegrity-retry-1.1.3 , text:Definition of a Retry}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:Core-TransactionalIntegrity-Receiver-1.1.3 , text:Receiver responsibilities}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:Core-TransactionalIntegrity-Sender-1.1.3 , text:Sender responsibilities}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-TIFailureScenarios-1.1.3 , text:Failure Scenarios}}</br>
&nbsp;&nbsp;&bull; {{pagelink:core-NFR-1.1.3 , text:Non functional Requirements}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-NFR-Requirements-1.1.3 , text:Requirements}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-NFR-Processing-Time-1.1.3 , text:Processing Times}}</br>
&nbsp;&nbsp;&bull; {{pagelink:Core-StandardPattern-1.1.3 , text:Standard Pattern - Composite Messages}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-SPComposites-1.1.3 , text:Standard Pattern for Composites}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-SPMessageHeader-1.1.3 , text:Message Headers}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-SPCancellation-1.1.3 , text:Cancellation}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-SPUseCaseCategories-1.1.3 , text:Use Case Categories}}</br>
&nbsp;&nbsp;&bull; {{pagelink:core-StandardPattern-appointment-1.1.3 , text:Standard Pattern - Appointments}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-StandardPattern-appointment-booking-1.1.3 , text:Booking}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-StandardPattern-appointment-update-1.1.3 , text:Updates}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-StandardPattern-appointment-cancel-1.1.3 , text:Cancellations}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-StandardPattern-appointment-rebook-1.1.3 , text:Rebook}}</br>
&nbsp;&nbsp;&bull; {{pagelink:core-StandardPattern-document-reference-1.1.3 , text:Standard Pattern - DocumentReference}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-StandardPattern-document-reference-Sender-1.1.3 , text:Sender}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-StandardPattern-document-reference-Receiver-1.1.3 , text:Receiver}}</br>
&nbsp;&nbsp;&nbsp;&nbsp;&bull; {{pagelink:core-StandardPattern-document-reference-interface-1.1.3 , text:Interface}}</br>

   

</details>

<hr>

# End to end workflow
This section covers the core elements of workflow outlined within the Booking and Referral Standard. There are two caveats when reading this:

- Workflow is dependent on its Application or use case, for example in 999 - CAS validation, there is no step to perform a booking. See the relevant use case page in the 
{{pagelink:applications, text:BaRS Applications}} section. 


- The order of workflow is interchangeable. It is possible to:
    - make a referral before a booking
    - refer without booking
    - book without referring

For more detail please visit the {{pagelink:core-EndToEndWorkflow-1.1.3, text: End to End Workflow}} section.

<hr>
<br>


# Core Functionality Requirements
BaRS should provide different functionality depending on:

- its {{pagelink:applications, text:Application or use case}}
- whether it acts as a sender or receiver


This list of functionality will expand in later versions of BaRS.

There are requirements in each of the central areas of functionality which every BaRS Application must adopt:

For more detail please visit the {{pagelink:core-FunctionalityRequirements-1.1.3, text: Core Functionality Requirements}} section.

<hr>
<br>

# Content Negotiation

Content Negotiation within BaRS leverages multiple variables within the CapabilityStatement and MessageDefinition to ensure that a Sender and a Receiver are Compatible. Though some of this is possible due to the Versioning Negotiation, Content Negotiation further builds on that concept with the capabilities published by the server and the identification of message definitions and use cases therein to ensure a workflow can be completed. 

For more detail please visit the {{pagelink:core-content-negotiation, text: Content Negotiation}} section.

<hr>
<br>

# BaRS FHIR usage
BaRS uses [FHIR](https://digital.nhs.uk/services/fhir-uk-core) to achieve interoperability between healthcare IT systems. This section explains how BaRS makes use of some key FHIR concepts which need to be understood by developers implementing the standard.  

For more detail please visit the {{pagelink:core-FHIRUsage-1.1.3, text: BaRS FHIR usage}} section.

<hr>
<br>

# Security and Authorisation

For more detail on Security and Authorisation, please visit the {{pagelink:core-Security-1.1.3, text: Security and Authorisation}} section.

<hr>
<br>

# Error Handling
There are multiple points where an error may occur to prevent booking and referral operations from completing successfully. This section provides error handling guidance for BaRS and its associated API. For More Detail on error handling, there is specific information on failure scenarios available in the {{pagelink:core-failure_scenarios-1.1.3}} section in addition to information included on this page.

For more detail please visit the {{pagelink:core-ErrorHandling-1.1.3, text: Error Handling}} section.

<hr>
<br>

# Transactional Integrity
Transactional integrity is employed to ensure data integrity is maintained between two parties. It helps ensure that the success or failure of a message is known and can be confirmed. 

For more detail please visit the {{pagelink:Core-TransactionalIntegrity-1.1.3, text:Transactional Integrity}} section.

<hr>
<br>

# Non Functional Requirements

The non functional requirements apply to all APIs designed to receive requests from BaRS. This includes sender systems receiving asynchronous responses and feedback, as well as receiving systems. All items detailed will be adhered to.

For more detail please visit the {{pagelink:core-NFR-1.1.3, text: Non Functional Requirements}} section.

<hr>
<br>

# Standard Pattern - Composite Messages
Most implementations of the BaRS that are applying the standard to support a particular use case or operational workflow will follow the same basic set of foundational operations with little deviation. 

In order to establish a guarantee of compatibility between different solutions compliant with the standard, **all** implementations **must** support all the underlying foundational operations and patterns.

For more detail please visit the {{pagelink:Core-StandardPattern-1.1.3, text: Standard Pattern - Composite Messages}} section.

<hr>
<br>

# Standard Pattern - Appointment

There are 4 capabilities that are required surrounding appointments. This section will provide information on how to meet them.

* The ability to book an appointment.
* The ability to cancel an appointment.
* The ability to update an appointment.
* The ability to rebook an appointment.

For more detail please visit the {{pagelink:core-StandardPattern-appointment-1.1.3, text: Appointment Standard Pattern}} section.

<hr>
<br>

# Standard Pattern - DocumentReference

In version 1.1.0 of the BaRS API Specification, functionality was added to accommodate the use of pointers (DocumentReference resources), to locate existing bookings and referrals.

The FHIR DocumentReference resource allows you to reference and locate clinical documents or resources. This section will walk you through the process of using a FHIR DocumentReference to find a resource's location and retrieve it.

For more detail please visit the {{pagelink:core-StandardPattern-document-reference-1.1.3, text: DocumentReference Standard Pattern}} section.

<hr>
<br>