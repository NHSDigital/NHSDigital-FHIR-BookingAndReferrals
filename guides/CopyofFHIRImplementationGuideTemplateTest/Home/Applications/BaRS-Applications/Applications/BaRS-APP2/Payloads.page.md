---
topic: APP2-Payloads
---

## {{page-title}}
The specific guidance around the use of key FHIR resources is described below. 

### MessageHeader Resource
{{pagelink:core-SPMessageHeader-1.1.3, text:Standard Patterns for BaRS Operations}} explains in detail how the **MessageHeader** resource **must** be used. 

The MessageHeader resource for the Booking Request should have the following resource elements set as follows:
* **MessageHeader.eventCoding** - **must** be populated with 'booking-request'
* **MessageHeader.reasonCode** - **must** be 'new' or 'update'
* **MessageHeader.focus** - **must** reference the Appointment FHIR resource
* **MessageHeader.definition** - **must** adhere to [Booking Request](https://simplifier.net/NHSBookingandReferrals/MessageDefinition-BARS-MessageDefinition-Booking-Request/~json) Message definition

The MessageHeader resource for the Referral Request should have the following resource elements set as follows:
* **MessageHeader.eventCoding** - **must** be populated with 'servicerequest-request'
* **MessageHeader.reasonCode** - **must** be 'new' or 'update'
* **MessageHeader.focus** - **must** reference the ServiceRequest FHIR resource
* **MessageHeader.definition** - **must** adhere to [Referral Request](https://simplifier.net/nhsbookingandreferrals/messagedefinition-bars-messagedefinition-servicerequest-request-referral) Message definition

### ServiceRequest Resource
The primary resource in a referral is the ServiceRequest resource. When the request 'message bundle' is created by the Sender and processed by the Receiver, this is the starting point from which the referral is understood. It provides either the detail or references to all key FHIR resources, for exmaple, the Patient, Encounter and Careplan. The guidance for this resource below goes into more element level detail. A key point when a Sender builds the referral FHIR 'message bundle' is to ensure the *MessageHeader.focus* references the ServiceRequest resource. 

There are two *coding* entries within *ServiceRequest.category* which are key to driving workflow:
1. Denotes the type of referral e.g. Transfer of care
2. Denotes the use case and must be populated with the relevant use case from [use-case CodeSystem](
https://simplifier.net/nhsbookingandreferrals/usecases-categories-bars
). e.g. 111 Online - ED, S&R - UTC. Please refer to the guidance in {{pagelink:core-SPUseCaseCategories-1.0.3, text:use-case categories}}

An important function of the ServiceRequest resource is to link the booking and referral when they are related in a workflow. If the booking is successfully made before the referral, the Sender will have the *Appointment.Id* value and this **must** be included as a relative reference, under *ServiceRequest.supportingInfo*, in the referral request. The element *ServiceRequest.supportingInfo* **may** also be used to provide referrence to other resources in the request i.e. Rejected Services. This is outlined in the element guidance below.

### Appointment 
The primary resource in a booking is the Appointment resource. When the request 'message bundle' is created by the Sender and processed by the Receiver, this is the starting point from which the booking is understood. It provide either the detail or references to all key FHIR resources. When a Sender builds the booking FHIR 'message bundle' they **must** ensure the *MessageHeader.focus* references the Appointment resource. 

An important function of the Appointment resource is to link the booking and referral when they are related in a workflow. If the referral is successfully made before the booking, the Sender will have the *ServiceRequest.Id* value (from the synchronous HTTP response) and this **must** be included as a relative reference, under *Appointment.basedOn*, in the booking request. 

### Encounter Resource
The Encounter is used to represent the interaction between a patient and healthcare service provider. It links with numerous other resources, to reflect the assessment performed. 

In the initial referral request, the Sender will include an Encounter resource as the container for their assessment, which established the need for the referral. This encounter **should** include a reference to the Sender's assessment under *encounter.identifier*. Additionally, the *encounter.episodeOfCare* **must** be populated with a 'Journey ID' reference which can be used in subsequent referrals to allow the audit of the route a patient took through service providers to resolve their initial request for care. 

A second Encounter resource is used to transfer the human readable reference of the newly created referral, at the Receiver side. When a referral request is made, the Receiver **should** include a new, secondary, encounter resource with the status of 'planned' in their synchronous HTTP response to the Sender's request. This new 'planned' encounter will have both an Id and an Identifier value, indicating the Receiver's human readable and local references, respectively. This secondary, 'planned', encounter is <ins>not</ins> mandatory and has a cardinality of 0..1, unlike the primary encounter resource (1..1)(See the Entity Relationship Diagram for reference). The human readable (Identifier) reference is intended to allow Senders to provide something to the patient which they can take between services to support consistent joined up care, although, it is also a useful link for the services themselves to use when discussing a patient's transition of care. The local (Id) reference is not intended to be human readable but rather machine readable.

### CarePlan Resource
The CarePlan resource is used in a referral request to communicate the assessment triage outcome and any associated clinical information, based on the assessment performed by the Sender. The Receiver will to utilise the detail in this resource to summarise what the previous assessment ascertained about the patient, to be used in any subsequent consultation with the patient.

Primarily, *careplan.activity* is the section which holds this information, whether it be coded or freetext. The *careplan.activity.outcomeCodeableConcept* is malleable enough to support the transmission of Pathways coded outcomes as well as clinical narrative. The element guidance for this resource below goes into the specific detail but, fundamentally, the Sender must include the selected Pathway, Symptom Group,  Symptom Discrimintator and Disposition (DX) code, along with the Pathways Assessment report. Further clinical narrative, provided outside of the Pathways assessment, can also be included under this element using 'text'.

### Flag Resource
The Flag resource is used to communicate prospective warnings of potential issues when providing care to the patient. The population of the Flag Resource is optional as not all subjects will have relevant issues.

BaRS Senders **should** populate Flag resources and **should** make adequate provision in their solution to support key flags in BaRS Application workflows, for example, Rejected Services, for this Application. When populating this resource, Senders **must** include both *flag.category* and *flag.code* values using the specific [BaRS CodeSystems](https://simplifier.net/nhsbookingandreferrals/~resources?category=CodeSystem&sortBy=DisplayName).

When a BARS Receiver processes information in a Flag resource;

* they **should** populate a flag in their system, if their solution supports that flag
* they **must** display the information in the Flag resource in a way that supports the associated workflow (i.e. the relevant end users can see it an act upon it)
* rendering of Flag information must be in line with the {{pagelink:Home/About-BaRS/BaRS-Principles-and-Prerequisites/Principles-for-rendering-BaRS-payloads.page.md, text:Principles for rendering BaRS Payload }}.

### Observation 
The Observation resource is used to carry assertions supporting the assessment performed by the Sender. In the BaRS UEC Applications, Senders **should** add clinical notes to the Careplan resource rather than Observation, especially where they expect a Receiver to act upon the information. 

There are specific instances where an Observation **must** be used to convey information and [exmaples](https://simplifier.net/nhsbookingandreferrals/~resources?category=Example&exampletype=Observation&sortBy=DisplayName) are provided to aid development: 
* Birth Sex **must** be transfered in a referral using Observation. This information **should** only be transferred when considered clincally relevant and it is not considered as demographic information, as administrative gender would be. It **should <ins>not</ins>** be included as an extension on the patient resource, as described in [UK Core](https://simplifier.net/hl7fhirukcorer4/ukcorepatient). 
* Estimated Age **must** be conveyed in an Observation.

### QuestionnaireResponse 
QuestionnaireResponse is optionally used to carry structured data in BaRS UEC Applications, specifically, to communicate: 
* references to **external sources** of clinical information, looked up during the Sender's assessment
* any **Rejected Services** by the patient prior to selection on the Receiver service

The extension *questionnaireresponse-reason* **must** be populated to indicate which data is contained within, as outlined in the resource element guidance below.

Using a nested set of *questionnaireResponse.item*, *questionnaireResponse.linkId* and *questionnaireResponse.answer* complex structured data can be generated and processed, by the Sender and Receiver, respectively. The element guidance for this resource below goes into detail but, essentially, the *item* and *linkId* can be continually nested to convey various types of information. The *item* indicates a new element, *linkId* provide the number of elements (within the *item*) and *answer* contains any the value, supported by many different data types.

### Consent 
In the BaRS UEC Applications the level of consent is stipulated to be for 'Direct Care' only. A referral **must** contain a Consent resource and it **must** adhere to the [example](https://simplifier.net/nhsbookingandreferrals/consent-example) provided under the BaRS FHIR assets. 

<hr>

<div markdown="span" class="alert alert-warning" role="alert"><i class="fa fa-warning"></i>
    <b> Important:</b> 
    The sections below show elements in key resources that extend UK Core. Where no table is present, the basic UK Core resource is used unaltered.
</div>
