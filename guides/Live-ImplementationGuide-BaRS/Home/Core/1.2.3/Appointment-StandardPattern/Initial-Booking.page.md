---
topic: core-StandardPattern-appointment-booking-1.2.2
---

## Appointment Resource

Below are examples of each of the described interactions. The appointment resource adheres to the [UKCore-Appointment](https://simplifier.net/HL7FHIRUKCoreR4/UKCore-Appointment) definition.

Any operations that modify an existing resource must perform a read before a write.  GET /Appointment/{id}

### Book
The method for the initial booking of an appointment depends on the {{pagelink:Home/Applications/BaRS-Applications, text:Application}} specific guidance within BaRS. Alternatively, booking an appointment can be used outside of use-cases supported by a BaRS Application, to fulfil a generic Appointment workflow, either way, the typical sequence of events is:

* Select the service to book an appointment with. 
* Confirm BaRS Capabilities.
* Request Available slots.
* Select a slot.
* Send a Request to book an appointment in that slot

<img src="https://raw.githubusercontent.com/NHSDigital/NHSDigital-FHIR-BookingAndReferrals/main/BaRS-Images/SequenceDiagrams/BaRS_Foundation_Book.drawio.svg" ></img>

Once the appointment is created, the Receiver is responsible for managing the pointer in the central Registry, as described {{pagelink:core-StandardPattern-document-reference-1.2.2, text: here}}.


