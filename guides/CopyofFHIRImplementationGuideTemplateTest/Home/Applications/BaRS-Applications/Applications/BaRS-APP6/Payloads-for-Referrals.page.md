---
topic: APP6-Payloads
---

## {{page-title}}

<br>

## Referral Payload
The below details the specific guidance around the use of resources required to create a referral by the referral Sender. See [ServiceRequest - Request Referral](https://simplifier.net/nhsbookingandreferrals/messagedefinition-bars-messagedefinition-servicerequest-request-referral) message definition for details of resources required for this payload.

*Note that referral Senders will also have to build the capability to receive and process the Referral Response (Status update) payload.*

### MessageHeader Resource
For detailed information on the use of MessageHeader please refer to the {{pagelink:core-SPMessageHeader, text:Standard Pattern Message Header}}. 

The MessageHeader resource for the Referral Request should have the following resource elements set as follows:
* **MessageHeader.eventCoding** - **must** be populated with 'servicerequest-request'
* **MessageHeader.reasonCode** - **must** be 'new'
* **MessageHeader.focus** - **must** reference the ServiceRequest FHIR resource
* **MessageHeader.definition** - **must** adhere to [Referral Request](https://simplifier.net/NHSBookingandReferrals/MessageDefinition-BARS-MessageDefinition-ServiceRequest-Request-Referral/~json) Message definition

### ServiceRequest Resource
The 'focus' resource in a referral is the ServiceRequest resource. When the request payload (bundle) is created by the Sender and processed by the Receiver, this is the starting point from which the request is understood. It provides either the detail and references to all key FHIR resources, for example, the Patient, Encounter and Careplan. The guidance for this resource below provides more granular, element level, detail.

There are two *coding* entries within *ServiceRequest.category* which are key to driving workflow:
1. Denotes the type of referral e.g. Transfer of care
2. Denotes the use case and must be populated with the relevant use case from [use-case CodeSystem](
https://simplifier.net/nhsbookingandreferrals/usecases-categories-bars
). e.g. Out of area, Mutual Aid or Call Assist. Please refer to the guidance in {{pagelink:core-SPUseCaseCategories, text:use-case categories}}

Additionally, the *ServiceRequest.category.text* **must** be populated with details about the service request when the request is to support the Call Assist or Mutual Aid use cases.

### Encounter Resource
The Encounter is used to represent the interaction between a patient and healthcare service provider. It links with numerous other resources, to reflect the assessment performed. 

In the initial referral request, the Sender will include an Encounter resource as the carrier for the assessment, which established the need for the referral. This encounter **should** include a local human readable reference to the Sender's assessment under *encounter.identifier*. Additionally, the *encounter.episodeOfCare* **must** be populated with a 'Journey ID' reference which can be used in subsequent referrals to allow the audit of the route a patient took through service providers to resolve their initial request for care. 


When a referral request is made, the Receiver **should** include a new, secondary, encounter resource with the status of 'planned' in their synchronous HTTP response (200) to the Sender's request. This new 'planned' encounter will have an Identifier value, indicating *the Receiver's* local human readable reference. See the {{pagelink:APP6-EntityRelationshipDiagrams, text:Entity Relationship Diagrams}} for reference. The human readable (Identifier) reference is a useful link for the services to use when discussing a patient's transition of care. The local (Id) reference is not intended to be human readable but rather machine readable.


### Incident Location Resource ###
The Incident Location resource is used to transfer details of the incident location.

When the Sender populates the Incident Location resource:

*  They **must** populate the *Location.extension* with at least one property or non-property element from the following:
    *  Unique Property Reference Number (UPRN)
    *  Postcode Address Finder (PAF) key
    *  Eastings/Northings
    *  what3words
    
*  They *should* also populate the *Location.extension* with the percentage accuracy of the location
*  They **should** populate the *Location.address* for all property based locations
*  They **should** populate *Location.address.line* which is a repeatable element, with the order in which lines should appear in an address label
*  They **should** populate *Location.name* when there is a property name
*  They **should** populate *Location.address.text* with a text representation of the full address (including the address name), with each line separated by a comma

When a the Receiver processes information in an Incident Location resource:

*  They **should** consume and populate **all** address fields sent, into their system
*  They **must** display **all** address fields sent by the Sender


### Location Resource

The Location resource is used to transfer details of location types other than the Incident Location

When the Sender populates the Location resource:

*  They **must** populate the *Location.extension* with at least one property or non-property element from the following:
    *  Unique Property Reference Number (UPRN)
    *  Postcode Address Finder (PAF) key
    *  Eastings/Northings
    *  what3words
    
*  They **should** populate the *Location.address* for all property based locations. 
*  They **should** populate *Location.address.line* which is a repeatable element, with the order in which lines should appear in an address label
*  They **should** populate *Location.name* when there is a property name
*  They **should** populate *Location.address.text* with a text representation of the full address (including the address name), with each line separated by a comma

When a the Receiver processes information in a Location resource:

*  They **should** consume and populate **all** address fields sent, into their system
*  They **must** display **all** address fields sent by the Sender

*Note: The Patient Address is communicated in in the Patient resource and would only be replicated in the Location resource if it is also a secondary location e.g. Rendezvous point*

### CarePlan Resource
The CarePlan resource is used in a Referral Request to communicate the Sender's triage outcome and any associated clinical information, based on the assessment performed by the Sender. The Receiver will utilise the detail in this resource to review what the previous assessment ascertained about the patient, and to inform any subsequent action.

Primarily, *careplan.activity* is the section which holds this information, whether it be coded or free text. The *careplan.activity.outcomeCodeableConcept*  supports the transmission of AMPDS and Pathways coded outcomes and the clinical narrative. The element guidance for this resource below goes into the specific detail but, the Sender **must** include the following:
*  The selected AMPDS dispatch code and triage summary, or  
*  The Pathways, Symptom Group (SG),  Symptom Discriminator (SD) and Disposition (DX) codes, along with the Pathways consultation summary. 
*  Further clinical narrative, provided outside of the AMPDS or Pathways assessment, can also be included under this element using 'text'
*  The Ambulance Response Programme (ARP) priority code

The *CarePlan.period.start* is used to transfer the clock start time for dispatch and **must** be populated populated with Clock start date/Time Definition as per AmbSys specification.

* The *careplan.author.reference* **should** be populated with a reference to the *PractionerRole* when a triage has been validated or an assessment has been undertaken by a clinician. The *careplan.author.reference* **must not** be populated if the user undertaking the triage/assessment is NOT a clinical user.


### Flag (Scene safety)
The Flag (Scene Safety) resource is used to communicate safety information about the incident location. The *Flag.subject* is the *Incident Location* 

When populating this resource, Senders **must** include both *flag.category* and *flag.code* values using the specific [BaRS CodeSystems](https://simplifier.net/nhsbookingandreferrals/scene-safety-codes-bars)

When the scene is unsafe the *Flag.code.text* **must** be populated with the free text reason(s) that the scene is unsafe.

When a Receiver processes information in a Flag (Scene Safety) resource;

* they **should** populate a flag in their system schema, if their solution supports that flag
* they **must** display the information in the Flag (Scene Safety) resource (including *Flag.category* and *Flag.code*) in a way that supports the associated workflow (i.e. the relevant end users can see it and act upon it)
* rendering of Flag information must be in line with the {{pagelink:principles_prerequesites, text:Principles for rendering BaRS Payload }}.

### Flag Resource
The Flag resource is used to communicate prospective warnings of potential issues when providing care to the patient. The *Flag.subject* may be the *Patient* (e.g. Safeguarding concern) or the *Location* (e.g. location specific alerts). The population of the *Flag* is optional as not all subjects will have relevant issues.

The Sender **should** populate *Flag* resources and **should** make adequate provision in their solution to support key flags in BaRS Application workflows. When populating this resource, Senders **must** include both *flag.category* and *flag.code* values using the specific [BaRS CodeSystems](https://simplifier.net/nhsbookingandreferrals/~resources?category=CodeSystem&sortBy=DisplayName).

When a the Receiver processes information in a Flag resource;

* they **should** populate a flag in their system schema, if their solution supports that flag
* they **must** display the information in the Flag resource (including *Flag.category* and *Flag.code*) in a way that supports the associated workflow (i.e. the relevant end users can see it and act upon it)
* rendering of Flag information must be in line with the {{pagelink:principles_prerequesites, text:Principles for rendering BaRS Payload }}.

### Observation 
The Observation resource is used to carry assertions supporting the assessment performed by the Sender. Senders **should** add clinical notes to the Careplan resource rather than Observation, especially where they expect a Receiver to act upon the information. 

There are specific instances where an Observation **must** be used to convey information and [examples](https://simplifier.net/nhsbookingandreferrals/~resources?category=Example&exampletype=Observation&sortBy=DisplayName) are provided below to aid development: 
* Where Birth Sex is communicated it **must** be transferred in a Referral Request using an Observation. This information **should** only be transferred when considered clinically relevant and it is not considered as demographic information, as administrative gender would be. It **should <ins>not</ins>** be included as an extension on the patient resource, as described in [UK Core](https://simplifier.net/hl7fhirukcorer4/ukcorepatient). 
* Where Estimated Age is communicated it **must** be conveyed in an Observation.

### Consent 
The level of consent currently supported by BaRS is for 'Direct Care' only. In emergency care use cases this is usually implied consent. A Referral Request **must** contain a Consent resource and it **must** adhere to the [example](https://simplifier.net/NHSBookingandReferrals/8fc39b95-89a6-45fb-914f-1458a10e9e14/~json) provided under the BaRS FHIR assets. 

### Questionnaire
A Questionnaire is an organised collection of questions intended to solicit information from patients, providers or other individuals involved in the healthcare domain. They may be simple flat lists of questions or can be hierarchically organised in groups and sub-groups, each containing questions. The Questionnaire defines the questions to be asked, how they are ordered and grouped, any intervening instructional text and what the constraints are on the allowed answers. The results of a Questionnaire can be communicated using the QuestionnaireResponse resource.

The Questionnaire resource is used to covey the Pre Triage Sieve and Nature of Call (NOC) questions and the potential responses as detailed below:
#### Pre Triage Sieve

| Question                 | Answer| Code                  |
| -------------------------| ------| ----------------------|
|Is the patient breathing? |Yes      | 78064003  Breathing
|   |No      |1023001  Not Breathing
|Is the patient awake (conscious)?| Yes|428913001  No loss of consciousness|
| | No|419045004  Loss of consciousness|
|Is their breathing noisy?| Yes| 248573009  Noisy respiration|
| | No| 248573009  48348007 Normal breath sounds|

This is an [example](https://simplifier.net/NHSBookingandReferrals/9749ae76-28f7-4b8a-863f-aba64d19d678/~json) of the Pre triage Sieve questionnaire.

*Only the nationally agreed answers and associated codes in this table are valid to be sent. No locally defined responses can be sent.*

#### Nature of Call (NOC)

Nature of call types are nationally agreed by ECPAG for ASTs using both AMPDS and NHS Pathways as their CDSS. Receivers **MUST** be able to process and display NOC types and their associated code for both NHS Pathways and AMPDS NOC types  detailed below. 
##### AMPDS NOC Types

| Question                 | Answer (NOC type)| Code   |
| -------------------------| ------| -------|
|What is the Nature of Call?| Choking| CHOM|
|                           |Dangerous Haemorrhage|DAHM|
|                           | Drowning| DROM|
|                           | Fitting now| FINM|
|                           | Hanging| HANM|
|                           | HCP/IFT C1| HI1M|
|                           | Ineffective Breathing| INBM|
|                           | Major Trauma| MATM|
|                           | Maternity Complications| MACM|
|                           | Medical (unconscious)| MEUM|
|                           | Severe Allergic Reaction| SARM|
|                           | Trauma (unconscious)| TRUM|

This is an [example](https://simplifier.net/NHSBookingandReferrals/81599e54-c713-4f3e-bca9-90225657f18d/~json) of the Nature of Call questionnaire.

*Only the nationally agreed answers and associated codes in this table are valid to be sent. No locally defined responses can be sent.*

##### NHS Pathways NOC Types


| Question                 | Answer (NOC type) | Code   |
| -------------------------| ------| -------|
|What is the Nature of Call?| Anaphylaxis| ANAP|
|                           | Arrest/Peri Arrest (Cat1)|AP1P|
|                           | Asthma (life threatening)| ALTP|
|                           | Choking| CHOP|
|                           | Drowning| DROP|
|                           | Fitting Now| FINP|
|                           | Hanging| HANP|
|                           | HCP/IFT C1| HI1P|
|                           | Obstetric Emergency| OBEP|
|                           | Under 5 Severe Haemorrhage| 5SHP|
|                           | Under 16 unconscious| 16UP|
|                           | Unconscious pregnant >20 weeks | UNPP|

This is an [example](https://simplifier.net/NHSBookingandReferrals/81599e54-c713-4f3e-bca9-90225657f18d/~json) of the Nature of Call questionnaire.

*Only the nationally agreed answers and associated codes in this table are valid to be sent. No locally defined responses can be sent.*



### Questionnaire Response
The Questionnaire Response resource is used to convey the PTS and NOC responses given by the patient (or their representative).

The extension *questionnaireresponse-reason* **must** be populated to indicate which data is contained within, as outlined in the resource element guidance below.

Using a nested set of *questionnaireResponse.item*, *questionnaireResponse.linkId* and *questionnaireResponse.answer* complex structured data can be generated and processed, by the Sender and Receiver, respectively. The element guidance for this resource below goes into detail but, essentially, the item and linkId can be continually nested to convey various types of information, as guided by the corresponding questionnaire. The item indicates a new answer, linkId **must** correspond with the questionnaire question linkId, forging the relationship between the questionnaire and questionnaireResponse, and answer contains any the value recorded. The *questionnaireResponse.item.answer* datatype **must** correspond with that defined in the *questionnaire.item.answerOption*.

We have published examples of [Pre Triage Sieve](https://simplifier.net/NHSBookingandReferrals/Examples-QuestionnaireResponse-for-PTS/~json) and [Nature of Call](https://simplifier.net/NHSBookingandReferrals/Examples-QuestionnaireResponse-for-NOC/~json) questionnaire responses.

*Only the nationally agreed answers and associated codes in the associated Questionnaire are valid to be sent in the QuestionnaireResponse.* 

### Condition

The Condition resource is used to encapsulate the overall 'problem' the referral intends to resolve for the patient. The detail provided here underpins the rationale for the CarePlan and is a central resource for the Receiver looking for information about the patient and reason for referral.

The Condition resource is used to transfer the Presenting complaint. This is also referred to as:
* The Reason for Call (text)
* What's the problem? (text)

The key information about the 'problem' is comprised of two components within this Application, condition.category and condition.code. The category is used to qualify the code value, providing additional context to interpret the issue identified. For example, in this Application, the category will stipulate this is a 'presenting complaint', highlighting the provenance of the 'problem' for the Receiver to start their consultation. This is in addition to other specific status fields on the resource.


### Procedure
This resource is used to record the details of current and historical procedures performed on or for a patient. A procedure is an activity that is performed on, with, or for a patient as part of the provision of care.

The Procedure resource is used to communicate that Cardio Pulmonary Resuscitation by a bystander is being undertaken, and when it started.

### Task
The Task is used to direct the next action(s) required by the Sender making the referral, when the assessment has been undertaken without using NHS Pathways or AMPDS CDSS. Task supports in fulfilling Careplan, which also references it. The narrative within the payload starts with the assessment performed by the Sender (Encounter), identifying a 'problem' (Condition) which a plan of care (CarePlan) is established to address. The Sender is unable to support the plan of care so transitions responsibility, via a referral (ServiceRequest), while directing the next requested action (Task).

This Application utilises two elements within Task to direct the activity and time-frame, using *Task.code* and *Task.restriction.period*.

### Communication

The Communication resource is a conveyance of information from a sender to a receiver. The information can include encoded data, text and optionally a related Patient and a related Encounter.

In this application it is used to transfer Call Log information and Crew Notes.

<br>
<br>
<hr>

## Referral Cancellation Payload

The ability to cancel a referral is a core workflow in BaRS. For details on the use of the standard pattern for cancellation please see the following {{pagelink:core-SPCancellation, text:Standard Patterns - Cancellation}}.

<br>
<hr>    

