---
topic: core-StandardPattern-appointment-Introduction-1.2.1
---

# Standard Pattern - Appointments

<div markdown="span" class="alert alert-warning" role="alert"><i class="fa fa-warning"></i><b>Important:  Release information</b>
<p>This Section of the Implementation Guide is currently a preview, in an Alpha state and subject to change.</p>
</div>

## Introduction 

There are 4 capabilities that are required surrounding appointments. This section will provide information on how to meet them using the Appointment Resource.

* The ability to book an appointment.
* The ability to cancel an appointment.
* The ability to update an appointment.
* The ability to rebook an appointment.

## interface

The following table describes how the BaRS API accomodates these 4 capabilities using the /Appointment endpoint and the /Appointment/[id] endpoint

| Capability | Endpoint | VERB | Description |
|------------|-----------|-----|--------------|
| List   | /DocumentReference  | GET   | Using the {{pagelink:core-StandardPattern-document-reference-Introduction-1.1.4, text:DocumentReference}} pattern, a list of existing appointments for a patient can be viewed.  |
| View   | /Appointment/[id]  | GET   | This action, using the id from the List capability, will allow that specific Appointment Resource to be [retrieved](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_1_0#get-/Appointment). |
| Get Slots   | /Slots   | GET   | Obtain a list of available booking slots from a specified receiving system using the [GET /Slots endpoint](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_1_0#get-/Slot)  |
| Book | /Appointment or /$process-message | POST | This will invariably be a POST operation however the method for booking will depend on the BaRS Application/use case.|
| [Cancel](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_2_0#put-/Appointment/-id-) | /Appointment[id] | PUT| The cancel of a booking will be setting the status of the appointment to "cancelled" |
| [Update](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_2_0#put-/Appointment/-id-) | /Appointment[id] | PUT / PATCH| An update to an appointment will be a direct update to the existing resource |
| Rebook | Composite of Cancel and then Book | Composite | requesting a new booking and then cancelling the existing booking will constitute a rebook |

The specification for these operations can be found [here](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_2_0)

In line with the BaRS standard all operations used to modify a resource must be preceded by a read of the resource by means of a [GET](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_2_0#get-/Appointment/-id-) operation.
