---
topic: core-foundation-appointment-booking-1.1.3
---

## Appointment Resource

Below are examples of each of the described interactions. The appointment resource adheres to the [UKCore-Appointment](https://simplifier.net/HL7FHIRUKCoreR4/UKCore-Appointment) definitiion.

Any operations that modify an existing resource must perform a read before a write.  GET /Appointment/[id]

### Book
Book
The method for the initial booking of an appointment depends on the Application specific guidance within BaRS. However a typical sequence of events is:

* Select the service to book an appointment with. 
* Confirm BaRS Capabilities.
* Request Available slots.
* Select a slot.
* Send a Request to book an appointment in that slot


<img src="https://raw.githubusercontent.com/NHSDigital/booking-and-referral-media/master/src/images/SequenceDiagrams/BaRS_Foundation_Book.drawio.svg" ></img>


