---
topic: core-StandardPattern-appointment-update-1.3.1
---

### Update

Steps to update:

* Perform a [GET](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1.3.0#get-/Appointment/-id-) operation using the .id of the appointment to /Appointment/\{id\}. Alternatively, if the .id is not known, a search of the Registry can be undertaken following the {{pagelink:core-StandardPattern-document-reference-Sender-1.3.1, text: Document Reference Standard Pattern - Sender}}. NB: If a match cannot be obtained using this method the process of updating must be performed manually
* Update the Appointment resource as required. There is only currently support to alter .status and .reasonCode. NB: The .slot element of the resource must not be updated, if an alternative slot is required either the {{pagelink:core-StandardPattern-appointment-reschedule-1.3.1, text:Reschedule}} or {{pagelink:core-StandardPattern-appointment-rebook-1.3.1, text:Rebook}} processes must be followed
* Perform a [PUT](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1.3.0#put-/Appointment/-id-) operation using the id of the appointment to /Appointment/\{id\}

resource returned:
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
	"reasonCode": [
		{
			"coding": [
				{
					"system": "http://snomed.info/sct",
					"code": "165342003",
					"display": "Patient declined laboratory test (situation)"
				}
			]
		}
	],
	"description": "Reason for calling",
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

Request Body

```json
{
	"resourceType": "Appointment",
	"id": "aca94bdb-2e38-4399-9ece-2ba083ce65b5",
	"meta": {
		"lastUpdated": "2024-01-11T15:01:30.8185338+00:00",
		"profile": [
			"https://fhir.hl7.org.uk/StructureDefinition/UKCore-Appointment"
		]
	},
	"status": "booked",
	"reasonCode": [
		{
			"coding": [
				{
					"system": "http://snomed.info/sct",
					"code": "165332000",
					"display": "Laboratory test requested (situation)"
				}
			]
		}
	],
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
<img src="https://raw.githubusercontent.com/NHSDigital/NHSDigital-FHIR-BookingAndReferrals/main/BaRS-Images/SequenceDiagrams/BaRS_Foundation_Update.drawio.svg" ></img>
