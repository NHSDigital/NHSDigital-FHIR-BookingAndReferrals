---
topic: APP4-RequesterPayloads
---

# {{page-title}}

## Validation Request Payload
The below details the specific guidance around the use of resources required to create a Validation Request by the Requester. See [ServiceRequest - Request Validation](https://simplifier.net/nhsbookingandreferrals/messagedefinition-bars-messagedefinition-servicerequest-request-validation) message definition for details of resources required for this payload.

_Note that Requesters will also have to build the capability to receive and process the Validation Response payloads._

### MessageHeader Resource
For detailed information on the use of MessageHeader please refer to the {{pagelink:core-SPMessageHeader-1.1.3, text:Standard Pattern Message Header}}. 

The MessageHeader resource for the Validation Request should have the following resource elements set as follows:
* **MessageHeader.eventCoding** - **must** be populated with 'servicerequest-request'
* **MessageHeader.reasonCode** - **must** be 'new'
* **MessageHeader.focus** - **must** reference the ServiceRequest FHIR resource
* **MessageHeader.definition** - **must** adhere to [Validation Request](https://simplifier.net/NHSBookingandReferrals/MessageDefinition-BARS-MessageDefinition-ServiceRequest-Request-Validation/~json) Message definition

### ServiceRequest Resource
The 'focus' resource in a Validation Request is the ServiceRequest resource. When the request payload (bundle) is created by the Requester and processed by the Responder, this is the starting point from which the request is understood. It provides either the detail and references to all key FHIR resources, for example, the Patient, Encounter and Careplan. The guidance for this resource below provides more granular, element level, detail.

There are two *coding* entries within *ServiceRequest.category* which are key to driving workflow:
1. Denotes the type of referral e.g. Transfer of care
2. Denotes the use case and must be populated with the relevant use case from [use-case CodeSystem](
https://simplifier.net/nhsbookingandreferrals/usecases-categories-bars). e.g. 999- CAS Validation. Please refer to the guidance in {{pagelink:core-SPUseCaseCategories-1.0.3, text:use-case categories}}

Additionally, the *ServiceRequest.occurrencePeriod* **must** be populated with the time by which the receiving service must complete the validation (validation breach time).

### Encounter Resource
The Encounter is used to represent the interaction between a patient and healthcare service provider. It links with numerous other resources, to reflect the assessment performed. 

In the initial Validation Request, the Requester will include an Encounter resource as the carrier for the assessment, which established the need for the Validation Request. This encounter **should** include a local human readable reference to the Requester's assessment under *encounter.identifier*. Additionally, the *encounter.episodeOfCare* **must** be populated with a 'Journey ID' reference which can be used in subsequent referrals to allow the audit of the route a patient took through service providers to resolve their initial request for care. 


When a Validation Request is made, the Responder **should** include a new, secondary, encounter resource with the status of 'planned' in their synchronous HTTP response (200) to the Requester's request. This second Encounter resource is used to transfer the human readable reference of the newly created case, at the Responder end. This new 'planned' encounter will have an Identifier value, indicating *the Responder's* local human readable reference. (See the {{pagelink:APP3-EntityRelationshipDiagrams, text:Entity Relationship Diagram}} for reference). The human readable (Identifier) reference is a useful link for the services to use when discussing a patient's transition of care. The local (Id) reference is not intended to be human readable but rather machine readable.


### Location Resource ###
The Location resource is used to transfer details of the incident location.

When a BaRS Requester populates the Location resource:

*  They **must** populate the *Location.extension* with at least one property or non-property element from the following:
    *  Unique Property Reference Number (UPRN)
    *  Postcode Address Finder (PAF) key
    *  Eastings/Northings
    *  what3words

*  They **should** populate the *Location.address* for all property based locations. 
*  They **should** populate *Location.address.line* which is a repeatable element, with the order in which lines should appear in an address label
*  They **should** populate *Location.name* when there is a property name
*  They **should** populate *Location.address.text* with a text representation of the full address (including the address name), with each line separated by a comma

When a BaRS Responder processes information in a Location resource:

*  They **should** consume and populate **all** address fields sent, into their system
*  They **must** display **all** address fields sent by the Requester


### CarePlan Resource
The CarePlan resource is used in a Validation Request to communicate the 999 AST triage outcome and any associated clinical information, based on the assessment performed by the Requester. The Responder will utilise the detail in this resource to review what the previous assessment ascertained about the patient, and to inform any subsequent consultation with the patient.

Primarily, *careplan.activity* is the section which holds this information, whether it be coded or free text. The *careplan.activity.outcomeCodeableConcept*  supports the transmission of AMPDS and Pathways coded outcomes and the clinical narrative. The element guidance for this resource below goes into the specific detail but, fundamentally, the Requester must include the following:
*  The selected AMPDS dispatch code and triage summary, or  
*  The Pathways, Symptom Group (SG),  Symptom Discriminator (SD) and Disposition (DX) codes, along with the Pathways consultation summary. 
*  Further clinical narrative, provided outside of the AMPDS or Pathways assessment, can also be included under this element using 'text'
*  The Ambulance Response Programme (ARP) priority code

The *CarePlan.period.start* is used to calculate the clock start time for dispatch and **must** be populated populated with Clock start date/Time Definition as per AmbSys specification.

### Flag Resource
The Flag resource is used to communicate prospective warnings of potential issues when providing care to the patient. The *Flag.subject* may be the *Patient* (e.g. Safeguarding concern) or the *Location* (e.g. Scene safety). The population of the *Flag* is optional as not all subjects will have relevant issues.

BaRS Requesters **should** populate *Flag* resources and **should** make adequate provision in their solution to support key flags in BaRS Application workflows, for example, Scene Safety. When populating this resource, Requesters **must** include both *flag.category* and *flag.code* values using the specific [BaRS CodeSystems](https://simplifier.net/nhsbookingandreferrals/~resources?category=CodeSystem&sortBy=DisplayName).

When a BaRS Responder processes information in a Flag resource;

* they **should** populate a flag in their system schema, if their solution supports that flag
* they **must** display the information in the Flag resource (including *Flag.category* and *Flag.code*) in a way that supports the associated workflow (i.e. the relevant end users can see it and act upon it)
* rendering of Flag information must be in line with the {{pagelink:principles_prerequesites, text:Principles for rendering BaRS Payload }}.

### Observation 
The Observation resource is used to carry assertions supporting the assessment performed by the Requester. Requesters **should** add clinical notes to the Careplan resource rather than Observation, especially where they expect a Responder to act upon the information. 

There are specific instances where an Observation **must** be used to convey information and [examples](https://simplifier.net/nhsbookingandreferrals/~resources?category=Example&exampletype=Observation&sortBy=DisplayName) are provided below to aid development: 
* Where Birth Sex is communicated it **must** be transferred in a Validation Request using Observation. This information **should** only be transferred when considered clinically relevant and it is not considered as demographic information, as administrative gender would be. It **should <ins>not</ins>** be included as an extension on the patient resource, as described in [UK Core](https://simplifier.net/hl7fhirukcorer4/ukcorepatient). 
* Where Estimated Age is communicated it **must** be conveyed in an Observation.

### Consent 
The level of consent currently supported by BaRS is for 'Direct Care' only. In emergency care use cases this is usually implied consent. A Validation Request **must** contain a Consent resource and it **must** adhere to the [example](https://simplifier.net/NHSBookingandReferrals/8fc39b95-89a6-45fb-914f-1458a10e9e14/~json) provided under the BaRS FHIR assets. 
<br>
<br>
<hr>

## Validation Cancellation Payload

The ability to cancel a Validation Request is a core workflow in BaRS. For details on the use of the standard pattern for cancellation please see the following {{pagelink:core-SPCancellation-1.1.3, text:Standard Patterns - Cancellation}}.

<br>

<hr>
<div markdown="span" class="alert alert-warning" role="alert"><i class="fa fa-warning"></i>
    <b> Important:</b> 
    The sections below show elements in key resources that extend UK Core. Where no table is present, the basic UK Core resource is used unaltered.
</div>