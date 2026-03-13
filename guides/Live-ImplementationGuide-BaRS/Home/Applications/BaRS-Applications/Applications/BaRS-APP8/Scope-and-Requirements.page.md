---
TOPIC: APP8-ScopeAndRequirements
---

## {{page-title}}

### Scope Overview
This BaRS Application (Referrals from Advice and Guidance to eRS broker, Application 8) supports the following use case(s) ONLY:
- Advice and Guidance referring into eRS

The payload and workflow have been designed to support this service. Other {{pagelink:applications, text:BaRS Applications}} offer scope for alternative use cases.

### Functional Scope
**Directing the referral (without Service Discovery)**
- Direct to eRS static value 

**Referral**
- A referral in this Application is a request for care, on behalf of an individual, from a sending service to a broker 
- The referral can be sent without having to establish the capacity of the receiving service
- The referral will contain primarily clinical information, indicating the need of the individual and **must** state the anticipated action required by the receiving service (see Task FHIR resource)
- A list of healthcare services which can support the patient/client need are offered to the broker to direct the next step in care

**API-M**
- All requests and responses associated with BaRS must occur through the BaRS API Proxy

**Constraints**
- No guidance is provided on the display of referral information beyond the {{pagelink:principles_prerequesites, text:Principles for rendering BaRS Payload}}
- Consent within BaRS will be for Direct-Care only 
- Certificates for Receiving messages to use nhs.uk domains only
- Receiving endpoints are to be internet facing
- Clincial Constraints exist - See Hazard Log
- No element level 'updates' to requests are supported. A new request must be generated to change information in the referral request
- No digital support to remove or cancel a referral are offered (this would need to be achieved manually)
- Where an Online Consultation or other self assessment tool is used to refer, the referral must be verified by a human representative of the sending organisation before the request is made

### Requirements

**Directing a referral** 
- The service **must** support a unique identifier which the Sender is configured with to engage in the BaRS referral workflow

**Referral** 
- TBC

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
- Suppliers **must** adhere to the {{pagelink:core-ErrorHandling-1.3.1, text:error handling guidance}} 


### Non Functional 
- Suppliers **must** adhere to the {{pagelink:core-NFR-1.3.1, text:non functional requirements}}

