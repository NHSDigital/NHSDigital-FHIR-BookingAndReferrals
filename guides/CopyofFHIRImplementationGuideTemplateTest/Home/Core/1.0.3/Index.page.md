---
topic: design-core-1.1.3
---

# BaRS Core 1.0.3

BaRS consists of BaRS Core that provides a core set of functionality and BaRS Applications that provide distinct functionality for each use case.

You will find here a set of documentation, specifications and services that describe and support all the fundamental components of the standard that are always the same for all use cases or care journeys. Examples include the underlying capabilities and patterns and transport layer elements such as security, authorisation and access control.

<details>
<summary>> <b class="barslink">Expand for full Core directory</b></summary>
{{index:current}}
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