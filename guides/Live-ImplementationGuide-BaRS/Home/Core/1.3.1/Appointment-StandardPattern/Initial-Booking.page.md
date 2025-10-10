---
topic: core-StandardPattern-appointment-booking-1.3.1
---

## Appointment Resource

Below are examples of each of the described interactions. The appointment resource adheres to the [UKCore-Appointment](https://simplifier.net/HL7FHIRUKCoreR4/UKCore-Appointment) definition.

Any operations that modify an existing resource must perform a read before a write, as outlined below.

### Book
Making an initial booking through Appointment Management Foundation, outside of the prescribed BaRS Applications, must follow the workflow outlined using the discete [booking endpoints](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1.3.0#post-/Appointment). 

If undertaking a booking within the context of an Application, the guidance stated there takes precedence over this documentation. NB: BaRS Applications are likely to utilise the [$process-message](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1.3.0#post-/$process-message) endpoint (contact BaRS Team for guidance on use outside of the published Applications - <bookingandreferralstandard@nhs.net>), rather than independent resources. Steps to perform an initial booking:

* {{pagelink:core-EndToEndWorkflow-ServiceDiscovery-1.3.1, text:Select the service}} to book an appointment with
* Confirm BaRS [Capabilities](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1.3.0#get-/metadata)
* [Request Available slots](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1.3.0#get-/Slot)
* Select a slot
* Perform a [PUT](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1.3.0#post-/Appointment) operation to complete the booking NB: the returned Appointment.id for future operations

Request Body

```json
{
	"resourceType": "Appointment",
    "id":"aca94bdb-2e38-4399-9ece-2ba083ce65b5",
	"meta": {
		"lastUpdated": "2024-01-11T15:01:30.8185338+00:00",
		"profile": [
			"https://fhir.hl7.org.uk/StructureDefinition/UKCore-Appointment"
		]
	},
	"status": "booked",
    "slot": [
        {
            "reference": "Slot/deb4c4b3-870b-4599-84df-5e54cef7afda"
        }
    ],
	"description": "Reason for calling",
	"start": "2024-02-12T12:30:30+00:00",
	"end": "2024-02-12T12:40:30+00:00",
	"created": "2024-10-08T15:01:30+00:00",
	"participant": [
		{
			"actor": {
				"reference": "Patient/788660eb-d2c9-4773-abd4-318484673fb2"
			},
			"status": "accepted"
		}
	]
}
```

<img src="https://raw.githubusercontent.com/NHSDigital/NHSDigital-FHIR-BookingAndReferrals/main/BaRS-Images/SequenceDiagrams/BaRS_Foundation_Book.drawio.svg" ></img>

Once the appointment is created, the Receiver is responsible for managing the pointer in the central Registry, as described in {{pagelink:core-StandardPattern-document-reference-1.3.1, text: Document Reference Standard Pattern}}.


