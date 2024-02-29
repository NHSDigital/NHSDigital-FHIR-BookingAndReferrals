## {{page-title}}

## Delete once anything usefull has been removed.

### Overview
This page provides guidance for implementing the Booking and Referral Standard (BaRS) specifically for referrals into Clinical Assessment Services (CAS). It should be used alongside the {{pagelink: design-core ,text:BaRS Core implementation guide}} and Payload Definition Library when developing to the standard.

Whilst the goal for this BaRS Application is to support any referral into a CAS, the initial first of type use case is to support a referral from a 999 Ambulance Service Trust (AST) into a CAS for consultation. This is for cases with a non-ambulance triage outcome (also known as CAT5) that require input from a CAS clinician.

Please note that this Application does not support 999 AST cases with an ambulance triage outcome that require validating by a CAS clinician. Please see the {{pagelink:app-uec3}} Application for this use case.

### Workflow

{{render:Case-Transfer---Simplified.drawio--1}}

This details a referral into CAS generic workflow: 

- Prior to referral the sending service will undertake an assessment of the patient to determine whether they need referring into a CAS for the next step of their journey. This assessment may be undertaken by a clinician or a non-clinician supported by an approved Clinical Decision Support System (CDSS). 
- The sending service will then identify a suitable CAS based on the patient’s clinical needs and location. Service discovery will typically involve the use of a Service Directory (e.g. UEC DOS) or a local service map to ascertain the ServiceID.
- The Service ID is used to query the BaRS endpoint catalogue to identify the receiving CAS system's endpoint details.
- The sending service will send the referral to the CAS, including the information required by a CAS Clinician to continue the patent's clinical care.
- The CAS system will acknowledge the referral on receipt.
- Prior to the consultation the case will typically be posted to a queue for prioritisation, based on information in the referral.
- The CAS Clinician will contact the patient, or their representative, utilising information in the referral message, then undertake the consultation. The consultation will be informed by the clinical information sent by the referring service. This will be recorded in the CAS system.
- On completion of the consultation the next action is performed. This may include provision of care advice, onward referral to another service provider or an ambulance request for a worsening patient.

This details a referral into a CAS from a 999 Ambulance Service Trust (AST) for consultation:

- Prior to referral the 999 AST will undertake a triage of the patient to determine the acuity of the case. This will typically be undertaken by a call handler on the Computer Aided Dispatch system (CAD) using an approved Clinical Decision Support System (CDSS) such as NHS Pathways or AMPDS. For cases with a non-ambulance disposition (CAT5), local business rules will be applied to determine if the case meets the requirement for referral to a CAS for consultation.
- For cases requiring a referral to CAS, a suitable CAS is identified based on the patient’s clinical need and location. Service discovery will use local directories or UEC DOS to ascertain the ServiceID
- The Service ID is used to query the BaRS endpoint catalogue to identify the receiving CAS system's endpoint details.
- The 999-AST will send the referral to the CAS, including the information required by a CAS Clinician to continue the patent's clinical care. This will also include the JourneyID created at the patient's first contact.
- The CAS system will acknowledge the referral on receipt, after which the case may be closed by the 999 AST on the CAD. It should be noted that Duty of care is passed from the 999 AST with the referral and is considered accepted by the CAS on receipt of the acknowledgement.
- Prior to the consultation the case will typically be posted to a queue for prioritisation, based on information in the referral. This may be based on the call back time, determined locally or nationally based on the triage outcome codes. E.g. Where cases have a Pathways disposition (Dx) these are prioritised in accordance with the criteria specified in the IUC CAS service specification which sets out call-back times by Dx code.
- The CAS Clinician will contact the patient, or their representative, utilising information in the referral message, then undertakes a consultation which may include a triage. The consultation will be informed by the clinical information sent by the referring service. This will be recorded in the CAS system.
- On completion of the consultation the next action is performed. This may include provision of care advice with or without an electronic prescription (Hear and Treat), onward referral to another service provider or an ambulance request for a worsening patient.

### Application specific requirements

 A sender of a referral request must be capable of:

- searching for services with a directory    
- querying a receiver's message definition
- building a service request based on the message definition
- managing service requests made by themselves - create, read and update

A receiver of a referral request must be capable of:

- providing a FHIR resource message definition statement to indicate what a sender must include in a service request 
- managing service requests made by senders - create, read and update requests

### Data model endorsements

The referral information data model is based on user research with NHS 111 service providers, 999 Ambulance Service Trusts, Clinical Assessment Services and clinical and administrative Emergency Department staff.  We carried out this research in parallel with the [Professional Records Standards Body (PRSB)](https://theprsb.org/) who examined the wider brief of 'referrals from NHS 111 to any other care setting' 

For the  Referral into a CAS from a 999 Ambulance Service Trust (AST) for consultation use case, the data model is being endorsed by NHS England following consultation with the [Association of Ambulance Chief Executives (AACE)](https://aace.org.uk/),  National Ambulance Information Group (NAIG), National Ambulance Services Medical Directors' Group (NASMeD) and National Ambulance Digital Leaders Group (NADLG). 


### Payloads

The 999-CAS Referral Application uses the following payloads:

{{pagelink:Home/Build/PayloadDefinitions/Referral-Request-Payload.page.md}}

{{pagelink:Home/Build/PayloadDefinitions/Referral-Response-Payload.page.md}}

Note the Application specific guidance:

{{pagelink:Home/Build/PayloadDefinitions/999-AST-to-CAS-Referral.page.md}}