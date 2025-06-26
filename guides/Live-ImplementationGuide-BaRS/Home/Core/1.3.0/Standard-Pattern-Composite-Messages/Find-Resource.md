---
topic: core-SPFindResource-1.3.0
---


## {{page-title}}

A prerequisite, when undertaking any update routine, is to perform a read (GET) of either the booking or referral to be amended (including cancellation routines). This ensures the Sender has the most recent version of the resource being updated and verifies they can proceed with the workflow. For example, to engage in a cancellation workflow, the status of the entity being cancelled must currently be classed as 'active'. 

As a first step the Sender **must** obtain the (resource).Id of the booking (Appointment) or referral/validation (ServiceRequest) and they are several ways to do this. If the Sender made the original request, they will likely know this and can directly request the specific resource to check the status, using the GET (read) by Id endpoint. Alternatively, if they did not generate the original request (or there was a problem with the synchronous response being received) the full resource can be obtained by searching for active bookings or referrals for the patient, either by using the national identifier (NHS No.) or patient demographics (Name (as defined by [FHIR](https://simplifier.net/packages/hl7.fhir.r4.core/4.0.1/files/2834389 )), Date of Birth, Home Address Postcode). This will return a (FHIR) bundle of responses (typically, containing only one entry) which the Sender can match, based on dateTime (elements dependent on resource) and use-case category values, to identify the resource of interest. If the Sender cannot accurately match the resource they should advise the user the update cannot be performed and to revert to manual options instead. The diagram under 'Options for obtaining booking or referral' outlines the options above.

#### Options for obtaining booking or referral 

<br>
<br>
<p>
The below diagram details the options for obtaining the booking (Appointment) or referral/validation (ServiceRequest) resource, prior to update (including cancellation). The Sender <b>must</b> know the (resource).status and (resource).id values, as minimum, to build a valid update request.
</p>
<br>
<br>
<a href="https://raw.githubusercontent.com/NHSDigital/NHSDigital-FHIR-BookingAndReferrals/main/BaRS-Images/SequenceDiagrams/BaRS_StandardPattern_Cancellation_Find_Id.svg" target="_blank"><img src="https://raw.githubusercontent.com/NHSDigital/NHSDigital-FHIR-BookingAndReferrals/main/BaRS-Images/SequenceDiagrams/BaRS_StandardPattern_Cancellation_Find_Id.svg" width="1200"></img></a>
<br>
<br>
<hr>