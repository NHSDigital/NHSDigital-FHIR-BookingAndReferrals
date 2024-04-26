---
topic: core-foundation-appointment-Introduction-1.1.3
---

# Appointments

## Introduction 

There are 4 capabilities that are required surrounding appointments. This section will provide information on how to meet them.

* The ability to book an appointment.
* The ability to cancel an appointment.
* The ability to update an appointment.
* The ability to rebook an appointment.

## interface

The following table describes how the BaRS API accomodates these 4 capabilities using the /Appointment endpoint and the /Appointment/[id] endpoint

| Capability | Endpoint | VERB | Description |
|------------|-----------|-----|--------------|
| Book | /Appointment or /$process-message | POST | This will invariably be a POST operation however the method for booking will depend on the BaRS Application/use case.|
| [Cancel](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_2_0#put-/Appointment/-id-) | /Appointment[id] | PUT| The cancel of a booking will be setting the status of the appointment to "cancelled" |
| [Update](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_2_0#put-/Appointment/-id-) | /Appointment[id] | PUT / PATCH| An update to an appointment will be a direct update to the existing resource |
| Rebook | Composite of Cancel and then Book | Composite | requesting a new booking and then cancelling the existing booking will constitute a rebook |

The specification for these operations can be found [here](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_2_0)

In line with the BaRS standard all operations used to modify a resource must be preceded by a read of the resource by means of a [GET](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_2_0#get-/Appointment/-id-) operation.
