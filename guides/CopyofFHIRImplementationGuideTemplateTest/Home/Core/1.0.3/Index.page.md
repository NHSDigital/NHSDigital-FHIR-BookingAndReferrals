---
topic: design-core-1.0.3
---

# BaRS Core 1.0.3

BaRS consists of BaRS Core that provides a core set of functionality and BaRS Applications that provide distinct functionality for each use case.

You will find here a set of documentation, specifications and services that describe and support all the fundamental components of the standard that are always the same for all use cases or care journeys. Examples include the underlying capabilities and patterns and transport layer elements such as security, authorisation and access control.

<details>
<summary>> <b class="barslink">Expand for full Core directory</b></summary>

&bull;{{pagelink:design-core-1.0.3 , text: Core 1.0.3}}

&nbsp;&bull;{{pagelink:core-EndToEndWorkflow-1.0.3 , text:End to end workflow}}
&nbsp;&nbsp;&bull;{{pagelink:core-EndToEndWorkflow-ServiceDiscovery-1.0.3 , text:Service Discovery}}
&nbsp;&nbsp;&bull;{{pagelink:core-EndToEndWorkflow-BaRSAuth-1.0.3 , text:Authenticate with BaRS}}
&nbsp;&nbsp;&bull;{{pagelink:core-EndToEndWorkflow-API-1.0.3 , text:BaRS FHIR API}}
&nbsp;&nbsp;&bull;{{pagelink:core-EndToEndWorkflow-HTTPHeader-1.0.3 , text:HTTP Header}}
&nbsp;&nbsp;&bull;{{pagelink:core-EndToEndWorkflow-Routing-1.0.3 , text:Routing}}
&nbsp;&nbsp;&bull;{{pagelink:core-EndToEndWorkflow-Auth-1.0.3 , text:Authentication and Authorisation}}
&nbsp;&nbsp;&bull;{{pagelink:core-EndToEndWorkflow-Transactional-Integrity-1.0.3 , text:Transactional Integrity}}
&nbsp;&nbsp;&bull;{{pagelink:core-EndToEndWorkflow-HTTPResponseHeader-1.0.3 , text:HTTP Response Headers}}
&nbsp;&nbsp;&bull;{{pagelink:core-EndToEndWorkflow-Processing-1.0.3 , text:Processing Requests}}
&nbsp;&nbsp;&bull;{{pagelink:core-EndToEndWorkflow-Responses-1.0.3 , text:Responses}}
&nbsp;&nbsp;&bull;{{pagelink:core-EndToEndWorkflow-ReversingRoles-1.0.3 , text:Reversing Roles}}
&nbsp;&nbsp;&bull;{{pagelink:core-EndToEndWorkflow-AsyncWorkflow-1.0.3 , text:Asynchronous Workflow}}

&nbsp;&bull;{{pagelink:core-FunctionalityRequirements-1.0.3 , text:Core Functionality Requirements.}}
&nbsp;&nbsp;&bull;{{pagelink:core-FunctionalityRequirements-All-1.0.3 , text:All}}
&nbsp;&nbsp;&bull;{{pagelink:core-FunctionalityRequirements-Caching-1.0.3 , text:Caching}}
&nbsp;&nbsp;&bull;{{pagelink:core-FunctionalityRequirements-BookingSender-1.0.3 , text:Booking Sender}}
&nbsp;&nbsp;&bull;{{pagelink:core-FunctionalityRequirements-BookingReceiver-1.0.3 , text:Booking Receiver}}
&nbsp;&nbsp;&bull;{{pagelink:core-FunctionalityRequirements-ReferralSender-1.0.3 , text:Referral Sender}}
&nbsp;&nbsp;&bull;{{pagelink:core-FunctionalityRequirements-ReferralReceiver-1.0.3 , text:Referral Receiver}}

&nbsp;&bull;{{pagelink:core-FHIRUsage-1.0.3 , text:BaRS FHIR Usage}}
&nbsp;&nbsp;&bull;{{pagelink:core-FHIRUsage-Framework-1.0.3 , text:Frameworks}}
&nbsp;&nbsp;&bull;{{pagelink:core-FHIRUsage-REST-1.0.3 , text:REST}}
&nbsp;&nbsp;&bull;{{pagelink:core-FHIRUsage-FHIR-Operations-1.0.3 , text:FHIR Operations}}
&nbsp;&nbsp;&bull;{{pagelink:core-FHIRUsage-Process-Message-1.0.3 , text:$process-message}}
&nbsp;&nbsp;&bull;{{pagelink:core-FHIRUsage-bundle-1.0.3 , text:Bundle}}
&nbsp;&nbsp;&bull;{{pagelink:core-FHIRUsage-JourneyID-1.0.3 , text:Journey ID}}
&nbsp;&nbsp;&bull;{{pagelink:core-FHIRUsage-Time-1.0.3 , text:How to handle times}}
&nbsp;&nbsp;&bull;{{pagelink:core-FHIRUsage-LastUpdated-1.0.3 , text:LastUpdatedDate}}

&nbsp;&bull;{{pagelink:core-Security-1.0.3 , text:Security and Authorisation}}
&nbsp;&nbsp;&bull;{{pagelink:core-Security-Sender-1.0.3 , text:Sender}}
&nbsp;&nbsp;&bull;{{pagelink:core-Security-Oauth-1.0.3 , text:OAuth Endpoints}}
&nbsp;&nbsp;&bull;{{pagelink:core-Security-Receiver-1.0.3 , text:Receiver}}
&nbsp;&nbsp;&bull;{{pagelink:core-Security-Auth-1.0.3 , text:Authorisation}}
&nbsp;&nbsp;&bull;{{pagelink:core-ErrorHandling-1.0.3 , text:Error Handling}}
&nbsp;&nbsp;&bull;{{pagelink:core-ErrorHandling-Overview-1.0.3 , text:Overview}}
&nbsp;&nbsp;&bull;{{pagelink:core-ErrorHandling-IntS-1.0.3 , text:BaRS interactions(sending)}}
&nbsp;&nbsp;&bull;{{pagelink:core-ErrorHandling-OpOut-1.0.3 , text:OperationOutcome Example}}
&nbsp;&nbsp;&bull;{{pagelink:core-ErrorHandling-Diag-1.0.3 , text:Diagnostic Text}}
&nbsp;&nbsp;&bull;{{pagelink:core-ErrorHandling-Examples-1.0.3 , text:Example Errors}}
&nbsp;&nbsp;&bull;{{pagelink:core-ErrorHandling-SendResp-1.0.3 , text:Sender Responsibilities}}
&nbsp;&nbsp;&bull;{{pagelink:core-ErrorHandling-IntR-1.0.3 , text:BaRs interactions(receiving)}}
&nbsp;&nbsp;&bull;{{pagelink:core-ErrorHandling-RecResp-1.0.3 , text:Receiver responsibilities}}
&nbsp;&nbsp;&bull;{{pagelink:core-EHFailureScenarios-1.0.3 , text:Failure Scenarios}}
&nbsp;&nbsp;&bull;{{pagelink:core-failure_scenarios-1.0.3 , text:1.0.3}}
	 
&nbsp;&bull;{{pagelink:Core-TransactionalIntegrity-1.0.3 , text:Transactional Integrity}}
&nbsp;&nbsp;&bull;{{pagelink:Core-TransactionalIntegrity-Initial-1.0.3 , text:Initial Request}}
&nbsp;&nbsp;&bull;{{pagelink:Core-TransactionalIntegrity-Update-1.0.3 , text:Sending an update}}
&nbsp;&nbsp;&bull;{{pagelink:Core-TransactionalIntegrity-Feedback-1.0.3 , text:Feedback (response) requests}}
&nbsp;&nbsp;&bull;{{pagelink:Core-TransactionalIntegrity-Retry-1.0.3 , text:Retry Scenario}}
&nbsp;&nbsp;&bull;{{pagelink:Core-TransactionalIntegrity-Onward-1.0.3 , text:Onwards Referrals}}
&nbsp;&nbsp;&bull;{{pagelink:Core-TransactionalIntegrity-retry-1.0.3 , text:Definition of a Retry}}
&nbsp;&nbsp;&bull;{{pagelink:Core-TransactionalIntegrity-Receiver-1.0.3 , text:Receiver responsibilities}}
&nbsp;&nbsp;&bull;{{pagelink:Core-TransactionalIntegrity-Sender-1.0.3 , text:Sender responsibilities}}
&nbsp;&nbsp;&bull;{{pagelink:core-TIFailureScenarios-1.0.3 , text:Failure Scenarios}}
&nbsp;&nbsp;&bull;{{pagelink:core-NFR-1.0.3 , text:Non functional Requirements}}
&nbsp;&nbsp;&bull;{{pagelink:core-NFR-Requirements-1.0.3 , text:Requirements}}
&nbsp;&nbsp;&bull;{{pagelink:core-NFR-Processing-Time-1.0.3 , text:Processing Times}}
&nbsp;&nbsp;&bull;{{pagelink:Core-StandardPattern-1.0.3 , text:Standard Patterns for BaRS Operations}}
&nbsp;&nbsp;&bull;{{pagelink:core-SPComposites-1.0.3 , text:Standard Pattern for Composites}}
&nbsp;&nbsp;&bull;{{pagelink:core-SPMessageHeader-1.0.3 , text:Message Headers}}
&nbsp;&nbsp;&bull;{{pagelink:core-SPCancellation-1.0.3 , text:Cancellation}}
&nbsp;&nbsp;&bull;{{pagelink:core-SPUseCaseCategories-1.0.3 , text:Use Case Categories}}

&nbsp;&bull;{{pagelink:core-foundation-appointment-1.0.3 , text:Foundations - Appointments}}
&nbsp;&nbsp;&bull;{{pagelink:core-foundation-appointment-booking-1.0.3 , text:Booking}}
&nbsp;&nbsp;&bull;{{pagelink:core-foundation-appointment-update-1.0.3 , text:Updates}}
&nbsp;&nbsp;&bull;{{pagelink:core-foundation-appointment-cancel-1.0.3 , text:Cancellations}}
&nbsp;&nbsp;&bull;{{pagelink:core-foundation-appointment-rebook-1.0.3 , text:Rebook}}

&nbsp;&bull;{{pagelink:core-document-reference-1.0.3 , text:Foundations - Pointers}}
&nbsp;&nbsp;&bull;{{pagelink:core-document-reference-Sender-1.0.3 , text:Sender}}
&nbsp;&nbsp;&bull;{{pagelink:core-document-reference-Receiver-1.0.3 , text:Receiver}}
&nbsp;&nbsp;&bull;{{pagelink:core-document-reference-interface-1.0.3 , text:Interface}}

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

For more detail please visit the {{pagelink:core-EndToEndWorkflow-1.0.3, text: End to End Workflow section}} 

<hr>
<br>


# Core Functionality Requirements
BaRS should provide different functionality depending on:

- its {{pagelink:applications, text:Application or use case}}
- whether it acts as a sender or receiver


This list of functionality will expand in later versions of BaRS.

There are requirements in each of the central areas of functionality which every BaRS Application must adopt:

For more detail please visit the {{pagelink:core-FunctionalityRequirements-1.0.3, text: Core Functionality Requirements section}} 

<hr>
<br>

# Content Negotiation

Content Negotiation within BaRS leverages multiple variables within the CapabilityStatement and MessageDefinition to ensure that a Sender and a Receiver are Compatible. Though some of this is possible due to the Versioning Negotiation, Content Negotiation further builds on that concept with the capabilities published by the server and the identification of message definitions and use cases therein to ensure a workflow can be completed. 

For more detail please visit the {{pagelink:core-content-negotiation, text: Content Negotiation section}} 

<hr>
<br>

# BaRS FHIR usage
BaRS uses [FHIR](https://digital.nhs.uk/services/fhir-uk-core) to achieve interoperability between healthcare IT systems. This section explains how BaRS makes use of some key FHIR concepts which need to be understood by developers implementing the standard.  

For more detail please visit the {{pagelink:core-FHIRUsage-1.0.3, text: BaRS FHIR usage section}} 

<hr>
<br>

# Security and Authorisation

For more detail on Security and Authorisation, please visit the {{pagelink:core-Security-1.0.3, text: Security and Authorisation section}} 

<hr>
<br>

# Error Handling
There are multiple points where an error may occur to prevent booking and referral operations from completing successfully. This section provides error handling guidance for BaRS and its associated API. For More Detail on error handling, there is specific information on failure scenarios available in the {{pagelink:core-failure_scenarios-1.0.3}} section in addition to information included on this page.

For more detail please visit the {{pagelink:core-ErrorHandling-1.0.3, text: Error Handling section}} 

<hr>
<br>

# Transactional Integrity
Transactional integrity is employed to ensure data integrity is maintained between two parties. It helps ensure that the success or failure of a message is known and can be confirmed. 

For more detail please visit the {{pagelink:Core-TransactionalIntegrity-1.0.3, text:Transactional Integrity section}} 

<hr>
<br>

# Non Functional Requirements

The non functional requirements apply to all APIs designed to receive requests from BaRS. This includes sender systems receiving asynchronous responses and feedback, as well as receiving systems. All items detailed will be adhered to.

For more detail please visit the {{pagelink:core-NFR-1.0.3, text: Non Functional Requirements section}} 

<hr>
<br>

# Standard Patterns for BaRS Operations
Most implementations of the BaRS that are applying the standard to support a particular use case or operational workflow will follow the same basic set of foundational operations with little deviation. 

In order to establish a guarantee of compatibility between different solutions compliant with the standard, **all** implementations **must** support all the underlying foundational operations and patterns.

For more detail please visit the {{pagelink:Core-StandardPattern-1.0.3, text: Standard Patterns for BaRS Operations section}} 

<hr>
<br>

# Foundations - Appointment

There are 4 capabilities that are required surrounding appointments. This section will provide information on how to meet them.

* The ability to book an appointment.
* The ability to cancel an appointment.
* The ability to update an appointment.
* The ability to rebook an appointment.

For more detail please visit the {{pagelink:core-foundation-appointment-1.0.3, text: Appointment Foundations section}} 

<hr>
<br>

# Foundations - DocumentReference

In version 1.1.0 of the BaRS API Specification, functionality was added to accommodate the use of pointers (DocumentReference resources), to locate existing bookings and referrals.

The FHIR DocumentReference resource allows you to reference and locate clinical documents or resources. This section will walk you through the process of using a FHIR DocumentReference to find a resource's location and retrieve it.

For more detail please visit the {{pagelink:core-document-reference-1.1.3, text: DocumentReference Foundations section}} 

<hr>
<br>