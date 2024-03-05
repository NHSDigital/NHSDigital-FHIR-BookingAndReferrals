---
topic: APP4-ScopeAndRequirements
---
# {{page-title}}

## Scope Overview

This BaRS Application (application 4) covers only use cases:
* 999 Ambulance Service Trust (AST) Referral into Clinical Assessment Service (CAS) for Validation


The payloads and workflow have been designed to support these services. Other {{pagelink:applications, text:BaRS Applications}} offer scope for alternative use cases.

<br>
For this application we will be referring to the actors as 'Requester' and the 'Responder'. The Requester is the provider system that creates and sends the Validation Request to the Responder for completion. The Responder is the provider system that completes the validation request and responds back with the outcome of the assessment to the Requester. The table below summarises this.
<br>
<br>
<img src="https://raw.githubusercontent.com/NHSDigital/booking-and-referral-media/master/src/images/General/ValidationActors.svg" width="500"></img></a>
<br>
<br>

## Functional Scope

**Service Discovery**

* Establishing a service to direct requests to is a mandatory step in the workflow
* There is no restriction on the service discovery tools used. Any are capable of being supported whether national or proprietary
* The service **must** be configured within the BaRS infrastructure (Endpoint Catalogue) before requests can be made to the service

**Validation Request**
* A Validation Request is a request for the clinical validation of a triage outcome from one service to another 
* The Validation Request can be sent without having to establish the capacity the service offers
* The Validation Request  will contain primarily clinical information, indicating the need of the individual and **should** state the anticipated action required by the Responding service
* Supporting information, other than the assessment, is expected to be included in a Validation Request, if collected, including:
    * new or existing safeguarding concerns
    * locally held Special Patient Notes
    * external information sources used during initial assessment prior to referral
    * scene safety information
    * timing information to support the timely delivery of care and reporting

**Validation Responses**
* There are two supported Validation Responses in the workflow; Interim and Full
* The Interim Response has 2 purposes: 
    * Communication that the Validation Responder has started the assessment. 
        * When a CAS clinician starts to assess the patient an Interim Response **must** be sent to the Requester to covey that the status of the request has changed and is now 'in progress'
    * Communication that the Validation Responder has rejected the Validation Request
        * When CAS clinician cannot undertake the validation request (e.g. they fail to contact the patient within an appropriate timescale) an Interim Response **must** be sent to the Requester to convey that the status of the request has changed and is now 'cancelled'. It **should** include a reason for rejection.
        * On receipt of an Interim Response with an Encounter.status of 'cancelled' conveying the rejection of a Validation request, the Validation Requester *must* notify system users so they can take ownership of the case and perform the next activity.
* The Full Response contains the Validation Outcome, raising, lowering or preserving, the original ambulance category established by the 999 service, and **must** be sent to the Requester
* If a Validation Outcome raises the ambulance category to either a CAT 1 or CAT 2, the Responder **must** raise an ambulance with the Requesting 999 service using the existing CDA over ITK method
	* The new ambulance request, raised via ITK, **must** be included in the Full Response as an additional entity (FHIR Encounter)

**API-M**
* All requests and response associated with BaRS must occur through the BaRS API Proxy

**Constraints**
* Supporting use of Emergency Call Prioritisation Advisory Group (ECPAG) approved Clinical Decision Support Systems only (NHS Pathways, NHS Pathways Clinical Content Support (PaCCS) and Advanced Medical Priority Dispatch System (AMPDS)).
* No guidance provided on display of referral information beyond the {{pagelink:principles_prerequesites, text:Principles for rendering BaRS Payload}}.
* Consent within BaRS will be for Direct-Care only 
* Certificates for Receiving messages to use nhs.uk domains only.
* Receiving endpoints are to be internet facing.
* Clinical Constraints exist - See Hazard Log

## Requirements

**Service Discovery** 
* The service **must** support a unique identifier which the Sender extracts to engage in referral workflows

**Validation Request**
* The Responder **must** accept the Validation Request regardless of whether the patient is known to the service provider
* The Responder **must** accept potential patients who do **<ins>not</ins>** have a national validated identifier e.g. NHS Number
* The Requester **must** send incident location information as part of their request
* The Requester **must** send scene safety information as part of their request
* Any new or existing safeguarding concern, recorded as part of the assessment, **must** be included in the Validation Request
* The Responder **must** clearly identify any included safeguarding concern to the end user
* The Responder **must** accurately represent information made by the Sender to the end user
* The Requester **must** make available the human readable identifier for the referral, included in the HTTP synchronous response, to the end user
* Where the Validation Request was <ins>not</ins> successful, the Responder **must** send an appropriate response. See {{pagelink:failure_scenarios, text:failure scenarios}} for more detail
* Where the Validation Request was <ins>not</ins> successful, the Requester **must** present an appropriate message to the end user. See {{pagelink:failure_scenarios, text:failure scenarios}} for more detail

**Update Validation Request**
*	The Requester **must** be capable of updating any Validation Request made by them, within the current consultation or after the consultation event
*	The Requester **must** retrieve the Validation Request to be updated from the Responder prior to cancellation, to ensure they are working with the most up-to date version and it has not already been completed
*	The Requester **must** provide visible confirmation of the status returned by the Responder to the end-user , i.e. whether the original Validation Request was successfully updated or not
*	If the update fails, the Responder **must** respond with the most appropriately aligned error. See {{pagelink:failure_scenarios, text:failure scenarios}} for more detail
*	The Responder **must** store all previous versions of the Validation Request
*	The Requester **must <ins>not</ins>** be required to inform the patient of the updating of the Validation Request.  Business/clinical responsibility for informing the patient must remain with the Requester
*  The Requester  **should not** send updates after receiving an Interim Response


**Cancel Validation Request** 
*	The Requester **must** be capable of cancelling any Validation Request made by them, within the current consultation or after the consultation event
*	The Requester  **must** retrieve the Validation Request to be cancelled from the Responder prior to cancellation, to ensure they are working with the most up-to date version and it has not already been completed
*	The Requester  **must** provide visible confirmation of the status returned by the Responder to the end user , i.e. whether the original Validation Request was successfully cancelled or not
*	If the update fails the Responder **must** respond with the most appropriately aligned error 
*	The Responder **must** store all previous versions of the Validation Request
*	The Responder **must <ins>not</ins>** be required to inform the patient of the cancellation of the Validation Request.  Business/clinical responsibility for informing the patient must remain with the Requester

**Interim Validation Response**
*  The Responder **must** send an Interim Validation Response when the clinician starts the consultation in the CAS system. This **must not** be triggered by a clinician attempting to contact the patient or by a welfare call.
*  The Requester **must** process the Interim Validation Response, update the case in the CAD and display the status change to the end user.

**Validation Response**
*  The Responder **must** send an full Validation Response when the clinician has completed the consultation in the CAS system.
*  The Requester **must** process the Validation Response, update the case in the CAD and display the status change to the end user.
* The status on the Validation Response **must** indicate to the end user if a dispatch is required or not.
* The Requester **must** use status of the Validation Response to trigger system behaviour that ensures that cases that require a dispatch are acted on within an appropriate timescale, and cases that do not require a dispatch are closed
* The final triage should form part of the consultation history of the case in the CAD. 
* All triage instances should form part of the audit in the CAD.

**Incident Location**
*  The Requester  **must** include the incident location in the Validation Request
*  The Responder  **must** include the incident location in the Validation Response
*  All Locations **must** include a co-ordinate (Eastings/Northings, Lat/Long or What3Words equivalent) or a property location identifier (UPRN, Address and Postcode)

**Timings**
*  The Requester **must** send the Clock start date/Time (T5). Definition as per AmbSys specification
*  The Requester **must** send the validation breach time
*  The Responder **must** send the dispatch (or disposition) code identification datetime in the **Validation Response**:
    - If the Validation ARP code is the same or downgraded from the original 999 triage, this **must** be populated with the original 999 Clock start date/Time (T5).
    - If the Validation ARP code is upgraded from the original 999 triage this **must** be populated with the Dispatch/Disposition code identification date/time determined by the CAS


**Scene Safety**
*  The Requester **must** send scene safety information in the Validation Request
*  Where scene safety questions have not been asked, the *Flag* resource relating to scene safety  **must** be populated with 'UNK' unknown.
*  The Responder **should** populate the scene safety flag in their system and **must** display scene safety information to end users.
*  The Responder **must** send scene safety information in the Validation Response, including any updates.
*  The Requester **should** update their system scene safety flag with any updates in the Validation Response and **must** display scene safety updates to end users

**Contacts** 
* A minimum of one contact (patient or third party) with a contact method (phone, email, etc.) of phone **must** be provided in the Validation Request
* All contacts **must** have a rank
* There **must** be only one contact with a rank of 1
* All contacts **must** have at least one contact method (phone, email, etc.)
* All contact methods **must** have a rank
* There **must** be only one contact method with a rank of 1
* The contact ranked 1 and the contact method ranked 1 **must** be the primary callback for the Validation Request
<br>
<br>
### Audit
* Sufficient information around any activity through the API and subsequent BaRS workflow **must** be persisted to aid support incidents and audit requirements
<br>
<br>
### Error Handling 
* Suppliers **must** adhere to the {{pagelink:core-ErrorHandling, text:error handling guidance}} 
<br>
<br>
### Non Functional 
* Suppliers **must** adhere to the {{pagelink:core-NFR, text:non functional requirements}}
<br>
<br>
<hr>s