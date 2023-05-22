## {{page-title}}

### Overview

This page provides guidance for implementing the Booking and Referral Standard (BaRS) specifically for the referral from a 999 Ambulance Service Trust (AST) to a Clinical Assessment Service (CAS) to validate lower acuity ambulance triage outcomes, typically those mapped to an Ambulance Response Programme (ARP) priority category 3 or 4. It should be used alongside the {{pagelink: design-core, text: BaRS Core implementation guide}} and Payload Definition Library when developing to the standard.

### Workflow

{{render:Validation---simplified.drawio}}

- Prior to referral the 999 AST will undertake a triage of the patient to determine the acuity of the case. This will typically be undertaken by a call handler on the Computer Aided Dispatch system (CAD) using an approved Clinical Decision Support System (CDSS) such as NHS Pathways or AMPDS. For cases with a low acuity ambulance triage outcome (currently CAT3 and CAT4), local business rules are applied to determine if the case meets the requirement for clinical validation of triage outcome. These may be informed by the outcome of the NHSE/I Ambulance Validation Project.
- For cases meeting the criteria, a suitable CAS service for validation, is identified based on the patient’s location. Service discovery will be locally mapped or use UEC DOS to ascertain the ServiceID. This will be used to query the BaRS endpoint catalogue.
- The AST will send a validation request to the CAS which includes the Journey ID created at the patient’s first contact.
The case in the CAD is posted to a hidden/pending dispatch queue. If the case exceeds the validation breach time a failsafe process ensures that an ambulance is dispatched according to the original triage outcome.
- On receipt of the validation request, the CAS system sends an acknowledgement to the sending service.
- Cases are prioritised for validation on the CAS system clinical queue in order of the validation breach time, included in the BaRS validation request.
- The clinician calls back the patient (or their representative) based on the contact details in the validation request.
- As the clinician starts the validation, a status update is returned to the requesting 999 AST to inform them of the progress.
- The CAS clinician then validates the triage outcome (this may include re-triaging the patient or it may be a consultation) and communicates the outcome to the requesting 999 AST in a validation response message. 
- If the validation outcome upholds or downgrades the original triage outcome, but an ambulance is still required, the 999 AST Emergency Medical dispatcher (EMD) uses the information in the validation response message to dispatch an ambulance within the appropriate timescales. 
- If the validation outcome downgrades the original triage outcome to an onwards referral or Consult and Complete/Hear and Treat, this information is returned to the CAD in the Validation Response. The CAD acts on this information and removes the case from the hidden/pending dispatch queue.
- If the validation outcome is to upgrade to a CAT1/2 an ITK Ambulance Request is sent by the CAS to the 999 AST. The AST CAD treats this as a new case and calculates timings for ARP and Ambulance Quality Indicators (AQI) accordingly. In this scenario it will auto-dispatch according to local processes. The CAD sends an acknowledgement to the CAS which includes the case identifier of the new case. The CAS includes this in the validation response so that the CAD can mark the original case as a duplicate and remove from the dispatch queue. 

Note: Use of the ITK ambulance request message in this scenario is an interim flow for first of type implementations to manage the risk of change to the most urgent cases. This is pending the commission of the use of BaRS for the ambulance request message (including CAD to CAD) rather than the deprecated ITK ambulance request.



### Application specific requirements

A sender of a validation request must be capable of:

- searching for services with a directory   
- querying a receiver's message definition
- building a validation request based on the message definition
- managing validation requests made by themselves - create, read and update
- accepting a validation Response from an original request

A receiver of a validation request must be capable of:

- providing a FHIR resource message definition statement to indicate what a sender must include in a validation request 
- managing validation requests made by senders - create, read and update requests
- notifying 999 sender of a validation by sending a Validation Response from the CAS

### Data model endorsements

The referral information data model is based on user research with NHS 111 service providers, Clinical Assessment Services, 999 Ambulance Service Trusts and clinical and administrative Emergency Department staff.  We carried out this research in parallel with the Professional Records Standards Body  (PRSB) who examined the wider brief of 'referrals from NHS 111 to any other care setting' 

For the referral into a CAS from a 999 Ambulance Service Trust (AST) for validation use case, the data model is being endorsed by NHS England following consultation with  the Association of Ambulance Chief Executives (AACE),  National Ambulance Information Group (NAIG), National Ambulance Services Medical Directors' Group (NASMeD) and National Ambulance Digital Leaders Group (NADLG). 

### Payloads

The 999-CAS validation application uses the following payload:

Validation



