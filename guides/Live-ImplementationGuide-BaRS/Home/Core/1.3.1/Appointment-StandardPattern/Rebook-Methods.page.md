---
topic: core-StandardPattern-appointment-rebook-1.3.1
---

### Rebook

FHIR Guidance for [Rebook](https://hl7.org/fhir/R4/appointment.html)

#### Process for rebook
Rebooking through Appointment Management Foundation, outside of a prescribed BaRS Applications, must follow the workflow outlined. If undertaking a rebook within the context of an Application, the guidance stated there takes precedence over this documentation. NB: BaRS Applications are likely to utilise the [$process-message](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1.3.0#post-/$process-message) endpoint (contact BaRS Team <bookingandreferralstandard@nhs.net> for guidance on use of $process-message, outside of the published Applications), rather than independent resources. 

Steps to perform a rebook:

* {{pagelink:core-StandardPattern-appointment-cancel-1.3.1, text:Cancel existing booking}}
* {{pagelink:core-StandardPattern-appointment-booking-1.3.1, text:Rebook, following the initial booking workflow}}
* Once processed, the Receiver of the new booking must make a [POST](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1.3.0#post-/DocumentReference) request to create a new pointer in the central Registry, as described in {{pagelink:core-StandardPattern-document-reference-Receiver-1.3.1, text: Document Reference Standard Pattern - Receiver}}


<img src="https://raw.githubusercontent.com/NHSDigital/NHSDigital-FHIR-BookingAndReferrals/main/BaRS-Images/SequenceDiagrams/BaRS_Foundation_ReBook.drawio.svg" ></img>
