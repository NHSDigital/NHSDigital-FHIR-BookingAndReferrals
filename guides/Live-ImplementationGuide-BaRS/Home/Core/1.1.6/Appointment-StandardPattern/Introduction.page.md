---
topic: core-StandardPattern-appointment-Introduction-1.1.6
---

# Standard Pattern - Appointments

<div markdown="span" class="alert alert-warning" role="alert"><i class="fa fa-warning"></i><b>Important:  Release information</b>
<p>This Section of the Implementation Guide is currently a preview, in an Alpha state and subject to change.</p>
</div>

## Introduction 

The [BaRS API](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir) suite can be used where there is no specific use-case supported by the {{pagelink:Home/Applications/BaRS-Applications, text:Applications}} to fulfil generic Appointment workflows, referred to as Appointment Management Foundation. This section outlines the functionality supported, workflows involved and how these correspond with the [API Specification](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_1_0). 

This includes using {{pagelink:core-StandardPattern-document-reference-1.1.6, text: DocumentReference Standard Pattern}} to write pointers for Appointments to a central respository, commonly referred to as the Registry. 

The Appointment Management Foundation is based on {{pagelink:design-core-1.1.6, text:BaRS Core}} and an understanding of the central tenets is essential before beginning. This includes: - 
* {{pagelink:core-EndToEndWorkflow-1.1.6, text:End to end workflow }} - how Senders and Receivers, interacting through the central Proxy, negotiate compatibility and engage
* {{pagelink:core-EndToEndWorkflow-ServiceDiscovery-1.1.6, text:Service Discovery }} - every workflow must include the resolution of a receiving Service Identifier 
* {{pagelink:core-Security-1.1.6, text:Authentication and Authorisation }} - the central Proxy will handle Authentication but Authorisation is handled by Receivers
* {{pagelink:onboarding, text:Onboarding to environments }} - getting access to the central Proxy. This differs for Senders (OAuth) and Receivers (mTLS)

There are four functions that are required surrounding appointments. This section will provide information on how to meet them using the Appointment Resource.

* The ability to book an appointment.
* The ability to cancel an appointment.
* The ability to update an appointment.
* The ability to rebook an appointment.

## Interface

The following table describes how the BaRS API accomodates these four capabilities using the [/Appointment](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_1_0#post-/Appointment) endpoint and the [/Appointment/\{id\}](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_1_0#put-/Appointment/-id-) endpoint

| Capability | Endpoint | VERB | Description |
|------------|-----------|-----|--------------|
| [List](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_1_0#get-/DocumentReference) | /DocumentReference  | GET   | Using the {{pagelink:core-StandardPattern-document-reference-Introduction-1.1.6, text:DocumentReference}} pattern, a list of existing appointments for a patient can be viewed with the central Registry.  |
| [View](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_1_0#get-/Appointment/-id-) | /Appointment/\{id\}  | GET   | This action, using the id from the List capability, will allow that specific Appointment Resource to be [retrieved](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_1_0#get-/Appointment/-id-) from the healthcare service who owns it. |
| [Get Slots](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_1_0#get-/Slot) | /Slots   | GET   | Obtain a list of available booking slots from a specified receiving system using the [GET /Slots endpoint](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_1_0#get-/Slot)  |
| [Book](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_1_0#post-/Appointment) | /Appointment or /$process-message | POST | This will be a POST operation, with a BaRS Application /$process-message is typically used, outside of supported use cases /Appointment is adopted.|
| [Cancel](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_1_0#put-/Appointment/-id-) | /Appointment/\{id\} | PUT| The cancel of a booking will be setting the status of the appointment to "cancelled". Cancel is also possible using /$process-message |
| [Update](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_1_0#put-/Appointment/-id-) | /Appointment/\{id\} | PUT / PATCH| An update to an appointment will be a direct update to the existing resource |
| [Rebook](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_1_0#post-/Appointment) | Composite of Cancel and then Book | Composite | Requesting a new booking and then cancelling the existing one will constitute a rebook |


In line with the BaRS standard all operations used to modify a resource must be preceded by a read of the resource by means of a [GET](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_2_0#get-/Appointment/-id-) operation.
