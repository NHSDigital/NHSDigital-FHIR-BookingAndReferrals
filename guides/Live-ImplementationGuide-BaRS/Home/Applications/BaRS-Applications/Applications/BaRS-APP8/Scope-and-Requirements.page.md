---
TOPIC: APP8-ScopeAndRequirements
---

## {{page-title}}

### Scope Overview
This BaRS Application (Referrals from Advice and Guidance to e-RS broker, Application 8) supports the following use case(s) ONLY:
* Improved Advice and Guidance to electronic-Referral Service (e-RS)
* 111Online to electronic-Referral Service (e-RS)
* NHS.UK to electronic-Referral Service (e-RS)



The payload and workflow have been designed to support these services. Other {{pagelink:applications, text:BaRS Applications}} offer scope for alternative use cases.

### Functional Scope

**Service Discovery**
- Establishing a service, or service shortlist, for onward care is a mandatory step in the workflow


**Directing the referral (independent of Service Discovery)**
- Direct to predefined value representing the broker 

**Referral**
- A referral in this Application is a request for care, on behalf of an individual, from a sending service to a broker 
- The referral can be sent without having to establish the capacity of the receiving service
- The referral will contain primarily clinical information, indicating the need of the individual and **must** state the anticipated action required by the receiving service (see Task FHIR resource)
- A list of healthcare services which can support the patient/client need are offered to the broker to direct the next step in care
* Supporting information, other than the assessment, is expected to be included in a referral, if collected, including:
    * new or existing safeguarding concerns
    * locally held Special Patient Notes
    * external information sources used during initial assessment prior to referral
    * timing information to support the timely delivery of care and reporting


**API-M**
- All requests and responses associated with BaRS must occur through the BaRS API Proxy

**Constraints**
- No guidance is provided on the display of referral information beyond the {{pagelink:principles_prerequesites, text:Principles for rendering BaRS Payload}}
- BaRS currently supports the communication of consent for direct care only
- Certificates for Receiving messages to use nhs.uk domains only
- Receiving endpoints are to be internet facing
- Clincial Constraints exist - See Hazard Log
- No element level 'updates' to requests are supported. A new request must be generated to change information in the referral request
- No digital support to remove or cancel a referral are offered (this would need to be achieved manually)
- The service discovery tool for establishing services for onward care must be the [e-RS Service Search API A010](https://digital.nhs.uk/developer/api-catalogue/e-referral-service-fhir#post-/STU3/HealthcareService/$ers.searchHealthcareServicesForPatient)

### Requirements

**Service Discovery** 
- Where more than one service is shortlisted, the maximum number of services allowed on a given shortlist is 20.

**Referral**
- The referral Receiver **must** accept the referral request regardless of whether the patient is known to the service provider
- The referral Receiver **must** only accept potential patients who do **<ins>have</ins>** a national validated identifier e.g. NHS Number
- The national identifier  **must** have a [verification status](https://simplifier.net/hl7fhirukcorer4/valueset-ukcore-nhsnumberverificationstatus) of 'Number present and verified'  otherwise, the referral Sender **must <ins>not</ins>** include it in the request
- Any new or existing safeguarding concern, recorded as part of the assessment, **must** be included in the referral Sender's request
- The referral Receiver **must** clearly identify any included safeguarding concern to the end user
- The referral Receiver **must** accurately represent information made by the Sender to the end user.
- The referral Sender **must** make available the human readable identifier for the referral, included in the HTTP synchronous response, to the end user
- Where the referral was <ins>not</ins> successful, the Receiver **must** send an appropriate response. See {{pagelink:core-failure_scenarios-1.4.0, text:failure scenarios}} for more detail
- Where the referral was <ins>not</ins> successful, the Sender **must** present an appropriate message to the end user. See {{pagelink:core-failure_scenarios-1.4.0, text:failure scenarios}} for more detail
- The referral Sender **must** indicate consent to share (for Direct Care) to the Receiver 
- The referral Sender **must** indicate the urgency (using the agreed codeset) of the request to the Receiver 


### Audit
- Sufficient information around any activity through the API and subsequent BaRS workflow **must** be persisted to aid support incidents and audit requirements


### Error Handling 
- Suppliers **must** adhere to the {{pagelink:core-ErrorHandling-1.4.0, text:error handling guidance}} 


### Non Functional 
- Suppliers **must** adhere to the {{pagelink:core-NFR-1.4.0, text:non functional requirements}}

