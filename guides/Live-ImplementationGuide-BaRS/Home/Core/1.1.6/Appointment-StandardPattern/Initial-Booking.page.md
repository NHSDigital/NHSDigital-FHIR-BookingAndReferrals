---
topic: core-StandardPattern-appointment-booking-1.1.6
---

## Appointment Resource

Below are examples of each of the described interactions. The appointment resource adheres to the [UKCore-Appointment](https://simplifier.net/HL7FHIRUKCoreR4/UKCore-Appointment) definition.

Any operations that modify an existing resource must perform a read before a write.  GET /Appointment/\{id\}

### Book
The method for the initial booking of an appointment depends on the {{pagelink:Home/Applications/BaRS-Applications, text:Application}} specific guidance within BaRS. Within BaRS Applications, making a booking will involve building a FHIR bundle and making a POST to the [$process-message](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_1_0#post-/$process-message) endpoint. Alternatively, booking an appointment can be used outside of use-cases supported by a BaRS Application, to fulfil a generic Appointment Management Foundation workflow against the discete [booking endpoints](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_1_0#post-/Appointment), either way, the typical sequence of events is:

* {{pagelink:core-EndToEndWorkflow-ServiceDiscovery-1.1.6, text:Select the service}} to book an appointment with. 
* Confirm BaRS [Capabilities](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_1_0#get-/metadata).
* [Request Available slots](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_1_0#get-/Slot).
* Select a slot.
* Send a Request to [book an appointment](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_1_0#post-/Appointment) in that slot

Request Body

```json
{
	"resourceType": "Appointment",
    "id":"aca94bdb-2e38-4399-9ece-2ba083ce65b5"
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

Once the appointment is created, the Receiver is responsible for managing the pointer in the central Registry, as described {{pagelink:core-StandardPattern-document-reference-1.1.6, text: here}}.


