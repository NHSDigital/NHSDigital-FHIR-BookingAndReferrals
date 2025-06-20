---
TOPIC: APP5-ScopeAndRequirements
---

## {{page-title}}

### Scope Overview
This BaRS Application (Referrals into Community Pharmacy, Application 5) supports the following use case(s) ONLY:
- Primary Care to Community Pharmacy (Pharmacy First)
- Primary Care to Pharmacy Contraception (Oral Contraception for supply of initial or repeat prescriptions for Combined Oral Contraceptive (COC) or Proestogen Only Pill (POP))
- Primary Care to Pharmacy Blood Pressure Check Service


The payload and workflow have been designed to support this service. Other {{pagelink:applications, text:BaRS Applications}} offer scope for alternative use cases.

### Functional Scope
**Service Discovery**
- Establishing a service to direct requests to is a mandatory step in the workflow
- There is no restriction on the service discovery tools used. Any are capable of being supported whether national or proprietary. However, the NHS England Directory of Services supports this application and futher details are provided in the 'Find a Service' section
- The service **must** be configured within the BaRS infrastructure (Endpoint Catalogue) before requests can be made 

**Referral**
- A referral is a request for care, on behalf of an individual, from one service to another 
- The referral can be sent without having to establish the capacity of the receiving service
- The referral will contain primarily clinical information, indicating the need of the individual and **must** state the anticipated action required by the receiving service (see Task FHIR resource)

**API-M**
- All requests and responses associated with BaRS must occur through the BaRS API Proxy

**Constraints**
- No guidance is provided on the display of referral information beyond the {{pagelink:principles_prerequesites, text:Principles for rendering BaRS Payload}}
- Consent within BaRS will be for Direct-Care only 
- Certificates for Receiving messages to use nhs.uk domains only
- Receiving endpoints are to be internet facing
- Clincial Constraints exist - See Hazard Log
- No element level 'updates' to requests are supported. A new request must be generated to change information in the referral request
- Where an Online Consultation tool is used to refer, the referral must be verified by a human representative of the sending organisation before the request is made
- Referrals to the Oral Contraception service must adhere to the [published policy specification](https://www.england.nhs.uk/long-read/nhs-pharmacy-contraception-service/) 
- Referrals to the Blood Pressure service must adhere to the [published policy specification](https://www.england.nhs.uk/primary-care/pharmacy/pharmacy-services/nhs-community-pharmacy-blood-pressure-check-service/) 


### Requirements

**Service Discovery** 
- The service **must** support a unique identifier which the Sender extracts to engage in the BaRS referral workflow

**Referral** 
- Clinical and non-clinical users **must** be capable of making referrals
- The referral Receiver **must** accept the referral request regardless of whether the patient is known to the service provider
- The referral Receiver **must** accept potential patients who do **<ins>not</ins>** have a national validated identifier e.g. NHS Number.
- Where a national identifier is included, it **must** have a [verification status](https://simplifier.net/hl7fhirukcorer4/valueset-ukcore-nhsnumberverificationstatus) of 'Number present and verified' or 'Number present but not traced', otherwise, the referral Sender **must <ins>not</ins>** include it in the request
- Any new or existing Individual Requirements e.g. needle phobia, wheelchair access etc., recorded as part of the assessment, **must** be included in the referral Sender's request
- The referral Receiver **must** clearly identify any included Individual Requirements to the end user
- The referral Receiver **must** accurately represent information made by the Sender to the end user 
- The referral Receiver **must** display the Sender organisation name and identifier (Note - This organisation may not be the patient's registered GP Surgery.)
- The referral Sender **must** include the Pharmacy Service that the request is intended for (from the defined list)
- The referral Sender **must** indicate consent to share (for Direct Care) to the Receiver 
- The referral Sender **should** indicate the urgency (providing timeframe within which included actions are expected to take place) of the request to the Receiver 
- The referral Sender **must** indicate novel medications, established during the latest assessment and not available on existing records, to the Receiver 
- The referral Sender **must** indicate novel allergies, established during the latest assessment and not available on existing records, to the Receiver 
- The referral Sender **must** indicate localised Special Patient Notes (SPNs) to the Receiver, if they hold any for the patient
- The referral Sender **must** include the sending organisation type (organization.type in FHIR) to indicate the referral entry method into a Receiver
- The referral Sender **should** include the Body Mass Index (BMI) of the patient being referred
- The referral Sender **should** include the service type when requesting a Blood Pressure service e.g. single check or monitoring over a period (ABPM)
- The referral Sender **should** include the current oral contraception medication a patient is prescribed when requesting a Oral Contraception service, if requesting ongoing (repeat) supply
- The referral Sender **must** make available the human readable identifier for the referral, included in the HTTP synchronous response, to the end user so they can share with the patient/third party
- Where the referral was <ins>not</ins> successful, the Receiver **must** send an appropriate response. See {{pagelink:core-failure_scenarios-1.3.0, text:failure scenarios}} for more detail.
- Where the referral was <ins>not</ins> successful, the Sender **must** present an appropriate message to the end user. See {{pagelink:core-failure_scenarios-1.3.0, text:failure scenarios}} for more detail.
- Update to amend a referral request is <ins>not</ins> supported. If a referral Sender wishes to change information in a request they **must** follow the re-refer workflow

**Cancel referral** 
-	The referral Sender **must** be capable of cancelling any referral made by them, within the current consultation or after the consultation event
-	The referral Sender **must** perform a read of the referral to be cancelled, from the referral Receiver, prior to cancellation to ensure they are working with the most up-to date information and it has not already been actioned
- Where the cancellation was <ins>not</ins> successful, the Receiver **must** send an appropriate response. See {{pagelink:core-failure_scenarios-1.3.0, text:failure scenarios}} for more detail.
- Where the cancellation was <ins>not</ins> successful, the Sender **must** present an appropriate message to the end user. See {{pagelink:core-failure_scenarios-1.3.0, text:failure scenarios}} for more detail.
-	The referral Receiver **must** store all previous versions of the referral
-	The referral Receiver **must <ins>not</ins>** be required to inform the patient of the cancellation of the referral.  Business/clinical responsibility for informing the patient remains with the referral Sender

**Re-refer** 
-	The referral Sender **must** be capable of re-referring within the current consultation or after the consultation event
-	If the patient recontacts the sending service after the sender's consultation has been completed, the patient **should** be reassessed prior to attempting to re-refer
-	The referral Sender **should** revoke the original referral prior to making a re-referral, whether within the current consultation or after the consultation event
-   Where the re-referral was <ins>not</ins> successful, the Receiver **must** send an appropriate response. See {{pagelink:core-failure_scenarios-1.3.0, text:failure scenarios}} for more detail.
-   Where the re-referral was <ins>not</ins> successful, the Sender **must** present an appropriate message to the end user. See {{pagelink:core-failure_scenarios-1.3.0, text:failure scenarios}} for more detail.
-	The referral Receiver **must <ins>not</ins>** be required to inform the patient of the cancellation, incurred as part of the re-refer process.  Business/clinical responsibility for informing the patient remains with the referral Sender

**Contacts** 
- A minimum of one contact (patient or third party) with a contact method (phone, email, etc.) of <ins>phone</ins> **must** be provided in referral requests
- All contacts **must** have a rank associated with them
- There **must** be only one contact with a rank of 1
- All contacts **must** have at least one contact method (phone, email, etc.)
- All contact methods **must** have a rank
- There **must** be only one contact method with a rank of 1
- The contact ranked 1 and the contact method ranked 1 **must** be the primary callback for the request


### Audit
- Sufficient information around any activity through the API and subsequent BaRS workflow **must** be persisted to aid support incidents and audit requirements


### Error Handling 
- Suppliers **must** adhere to the {{pagelink:core-ErrorHandling-1.3.0, text:error handling guidance}} 


### Non Functional 
- Suppliers **must** adhere to the {{pagelink:core-NFR-1.3.0, text:non functional requirements}}

