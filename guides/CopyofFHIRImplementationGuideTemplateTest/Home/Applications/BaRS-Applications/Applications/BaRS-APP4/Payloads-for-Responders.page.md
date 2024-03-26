---
topic: APP4-ResponderPayloads
---

# {{page-title}}

## Interim Validation Response Payload
This section provides guidance on the use of key resources, for the Responder to create an Interim Validation Response to return to the Requester. See [ServiceRequest - Response Validation Interim](https://simplifier.net/nhsbookingandreferrals/bars-messagedefinition-servicerequest-response-validation-interim) message definition for details of resources required for this payload.

_Note that Responders will also have to build the capability to receive and process the Validation Request and Cancellation payloads_
<br>

### MessageHeader Resource
For detailed information on the use of MessageHeader please refer to the {{pagelink:core-SPMessageHeader-1.1.3, text:Standard Pattern - Message Header}}. 

The MessageHeader resource in the Interim Validation Response should have the following resource elements set as follows:
* **MessageHeader.eventCoding** - **must** be populated with 'servicerequest-response'
* **MessageHeader.reasonCode** - **must** be 'new'
* **MessageHeader.focus** - **must** reference the Responder's current Encounter FHIR resource
* **MessageHeader.definition** - **must** adhere to [Interim Validation Response](https://simplifier.net/NHSBookingandReferrals/BARS-MessageDefinition-ServiceRequest-Response-Validation-Interim/~json) Message definition
* **MessgeHeader.Response** - **must** be the original request BundleID

### ServiceRequest Resource
The *ServiceRequest* reflects that sent by the Requester, and maintains the active state of the referral. The *ServiceRequest.status* at this point would stay as 'active'.

There are two *coding* entries within *ServiceRequest.category* which are key to driving workflow:
1. Denotes the type of referral e.g. Transfer of care
2. Denotes the use case and must be populated with the relevant use case from [use-case CodeSystem](
https://simplifier.net/nhsbookingandreferrals/usecases-categories-bars). e.g. Out of area, Mutual Aid or Call Assist. Please refer to the guidance in {{pagelink:core-SPUseCaseCategories-1.1.3, text:use-case categories}}


### Encounter Resource
The Responder's current *Encounter* is the focus resource in the Interim Validation Response. This was originally the 'planned' Encounter created by the Responder in the synchronous response to the Validation Request. 

This *Encounter* is used to represent the interaction between the patient and the Responder healthcare service provider. It links with numerous other resources, to reflect the activities performed in that encounter. 

When sending an Interim Validation Response to convey that the Responder is starting the assessment, the Responder **must**:
* Include the Responder's current *Encounter* as the focus resource of the Interim Validation Response
* Include an *encounter.status* of 'in-progress' to be set on the Responder's current *Encounter*. This is to indicate to the Requester that the validation activity has started.
* *encounter.reasonCode* to be included on the Responder's current *Encounter* to indicate that it is a response message (same code for both Interim and full Validation Response outcomes).

When sending an Interim Validation Response to convey that the Responder is rejecting the Validation Request, the Responder **must**:
* Include the Responder's current *Encounter* as the focus resource of the Interim Validation Response
* Include an *encounter.status* of 'cancelled' to be set on the Responder's current *Encounter*. This is to indicate to the Requester that the Validation Request has been rejected.
* *encounter.reasonCode* to be included on the Responder's current *Encounter* to indicate the reason for rejection.

<br>
<br>
<hr>

## Validation Response Payload
This section provides guidance on the use of key resources, for the Responder to create a Validation Response to return to the original Requester. See [ServiceRequest - Response Validation Full](https://simplifier.net/nhsbookingandreferrals/bars-messagedefinition-servicerequest-response-validation-full) message definition for details of resources required for this payload.

### MessageHeader Resource
For detailed information on the use of MessageHeader please refer to the {{pagelink:core-SPMessageHeader-1.1.3, text:Standard Pattern - Message Header}} for more information. 

The MessageHeader resource in the Interim Validation Response should have the following resource elements set as follows:
* **MessageHeader.eventCoding** - **must** be populated with 'servicerequest-response'
* **MessageHeader.reasonCode** - **must** be 'update' or 'new' if the Interim Validation Response was not sent
* **MessageHeader.focus** - **must** reference the Responder's current Encounter FHIR resource
* **MessageHeader.definition** - **must** adhere to [Validation Response](https://simplifier.net/nhsbookingandreferrals/bars-messagedefinition-servicerequest-response-validation-full) Message definition
* **MessgeHeader.Response** - **must** be the original request BundleID


### ServiceRequest Resource
The *ServiceRequest* is an echo of that sent by the Requester, and maintains the active state of the referral. The *ServiceRequest.status* at this point would stay as 'active'.  

### Encounter Resource

The Responder's current *Encounter* is the focus resource in the Validation Response. This was originally the 'planned' Encounter created by the Responder in the synchronous response to the Validation Request. 

This *Encounter* is used to represent the interaction between the patient and the Responder healthcare service provider. It links with numerous other resources, to reflect the activities performed in that encounter. 

When sending an Validation Response the Responder **must**:
* Include the Responder's current *Encounter* as the focus resource of the Validation Response
* Include an *encounter.status* of 'complete' to be set on the Responder's current *Encounter*. This is to indicate to the Requester that the validation activity has completed.
* *encounter.reasonCode* to be included on the Responder's current *Encounter* to indicate that it is a response message (same code for both Interim and full Validation Response outcomes).

A third Encounter **should** be included WHEN a validation request has resulted in a Cat1 or Cat2 outcome, AND ITK Ambulance Request has been sent to the Requester. The Requester **should** process the ITK request and merge this new case with the original case, on receipt of the Validation Response. 

### Location Resource
The Location resource is used to transfer details of the incident location. Incident location details may change during the course of the assessment and any additional or modified location details will be captured in the Responder system. The new and updated location details **must** be sent in the Validation Response. Where there are no changes the original Location details **must** be sent.

When a BARS Responder populates the Location resource:

*  They **must** populate the *Location.extension* with at least one property or non-property element from the following:
    *  Unique Property Reference Number (UPRN)
    *  Postcode Address Finder (PAF) key
    *  Eastings/Northings
    *  what3words

*  They **should** populate the *Location.address* for all property based locations. 
*  They **should** populate *Location.address.line* which is a repeatable element, with the the order in which lines should appear in an address label
*  They **should** populate *Location.address.name* when there is a property name
*  They **should** populate *Location.address.text* with a text representation of the full address (including the address name), with each line separated by a comma

When a BaRS Requester processes information in a Location resource in the Validation Response:

*  They **should** consume and populate **all** address fields sent, into their system
*  They **must** display *all* address fields sent by the sender


### CarePlan Resource
The CarePlan resource is used in the Validation Response to communicate to the Requester a summary of what was ascertained during the validation consultation. 

The *CarePlan.status* is used to drive workflow on the Requesters system. This **must** be populated with either a value of ‘complete’ or 'active'. If the status is 'complete' the Requester will know there is no further action required. If the status is 'active' the Requester will know there is an action required.

The *careplan.activity* holds the assessment information, whether it be coded or free text. The *careplan.activity.outcomeCodeableConcept* supports the transmission of Pathways coded outcomes and clinical narrative. The Responder must include the following:
*  The Pathways triage outcome including, Symptom Group (SG),  Symptom Discriminator (SD) and Disposition (DX) codes, along with the Pathways consultation summary
*  Further clinical narrative can also be included under additional instances of *careplan.activity.outcomeCodeableConcept.text*
*  The Ambulance Response Programme (ARP) priority code

The *CarePlan.period.start* is used to calculate the clock start time for dispatch and **must** be populated populated with the datetime of the identification of the dispatch code.
*  If the Validation ARP code is the same or downgraded from the original 999 triage, this **must* be populated with the Requester's Clock start date/Time Definition as per the AmbSys specification.
*  If the Validation ARP code is upgraded from the original 999 triage this **must** be populated with the Dispatch/Disposition code identification date/time determined by the CAS


### Flag Resource

The *Flag* resource is used to communicate prospective warnings of potential issues when providing care to the patient. The *Flag.subject* may be the *Patient* (e.g. Safeguarding concern) or the *Location* (e.g. Scene safety). The population of the *Flag* is optional as not all subjects will have relevant issues. *Flag* details may change during the course of the assessment and any additional or modified *Flag* details will be captured in the Responder system. The new and updated *Flag* details **must** be sent in the Validation Response. Where there are no changes the original *Flag* details **must** be sent.

BaRS Responders **should** populate *Flag* resources and **should** make adequate provision in their solution to support key flags in BaRS Application workflows, for example, Scene Safety. When populating this resource, Requesters **must** include both *flag.category* and *flag.code* values using the specific [BaRS CodeSystems](https://simplifier.net/nhsbookingandreferrals/~resources?category=CodeSystem&sortBy=DisplayName).

When a BaRS Requester processes information in a *Flag* resource in a Validation Response;

* they **should** populate a flag in their system schema, if their solution supports that flag
* they **must** display the information in the *Flag* resource (including *Flag.category* and *Flag.code*) in a way that supports the associated workflow (i.e. the relevant end users can see it and act upon it)
* rendering of *Flag* information must be in line with the {{pagelink:principles_prerequesites, text:Principles for rendering BaRS Payload }}.

### Observation 
The *Observation* resource is used to carry assertions supporting the assessment performed by the Responder. Responders **should** add clinical notes to the *CarePlan* resource rather than *Observation*, especially where they expect a Requester to act upon the information. 

There are specific instances where an Observation **must** be used to convey information and [examples](https://simplifier.net/nhsbookingandreferrals/~resources?category=Example&exampletype=Observation&sortBy=DisplayName) are provided to aid development: 
* Where Birth Sex is communicated it **must** be transferred in a Validation Response using Observation. This information **should** only be transferred when considered clinically relevant and it is not considered as demographic information, as administrative gender would be. It **should <ins>not</ins>** be included as an extension on the patient resource, as described in [UK Core](https://simplifier.net/hl7fhirukcorer4/ukcorepatient). 
* Where Estimated Age is communicated it **must** be conveyed in an Observation.

### Consent 
The level of consent currently supported by BaRS is for 'Direct Care' only. In emergency care use cases this is usually implied consent. A Validation Response **must** contain a Consent resource and it **must** adhere to the [example](https://simplifier.net/NHSBookingandReferrals/8fc39b95-89a6-45fb-914f-1458a10e9e14/~json) provided under the BaRS FHIR assets. 
<br>
<br>
<hr>
<div markdown="span" class="alert alert-warning" role="alert"><i class="fa fa-warning"></i>
    <b> Important:</b> 
    The sections below show elements in key resources that extend UK Core. Where no table is present, the basic UK Core resource is used unaltered.
</div>