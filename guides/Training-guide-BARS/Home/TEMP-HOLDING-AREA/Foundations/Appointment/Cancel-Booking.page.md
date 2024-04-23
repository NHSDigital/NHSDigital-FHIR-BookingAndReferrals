
### Cancel

To cancel an appointment:

* Perofrm a GET operation using the id of the appointment to /Appointment[id]
* Set the Appointment.status value to "cancelled"
* Perform a PUT operation using the id of the appointment to /Appointment[id]

resource returned:
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
            "reference": "urn:uuid:deb4c4b3-870b-4599-84df-5e54cef7afda"
        }
    ],
	"description": "Reason for calling",
	"start": "2024-02-12T12:30:30+00:00",
	"end": "2024-02-12T12:40:30+00:00",
	"created": "2024-10-08T15:01:30+00:00",
	"participant": [
		{
			"actor": {
				"reference": "urn:uuid:788660eb-d2c9-4773-abd4-318484673fb2"
			},
			"status": "accepted"
		}
	]
}
```

Request body:
```json
{
	"resourceType": "Appointment",
    "id":"aca94bdb-2e38-4399-9ece-2ba083ce65b5"
	"meta": {
		"lastUpdated": "2024-01-11T16:01:30.8185338+00:00",
		"profile": [
			"https://fhir.hl7.org.uk/StructureDefinition/UKCore-Appointment"
		]
	},
	"status": "cancelled",
    "slot": [
        {
            "reference": "urn:uuid:deb4c4b3-870b-4599-84df-5e54cef7afda"
        }
    ],
	"description": "Reason for calling",
	"start": "2024-02-12T12:30:30+00:00",
	"end": "2024-02-12T12:40:30+00:00",
	"created": "2024-10-08T15:01:30+00:00",
	"participant": [
		{
			"actor": {
				"reference": "urn:uuid:788660eb-d2c9-4773-abd4-318484673fb2"
			},
			"status": "accepted"
		}
	]
}
```
OR if the appointment was entered in error

Request body:
```json
{
	"resourceType": "Appointment",
    "id":"aca94bdb-2e38-4399-9ece-2ba083ce65b5"
	"meta": {
		"lastUpdated": "2024-01-11T16:01:30.8185338+00:00",
		"profile": [
			"https://fhir.hl7.org.uk/StructureDefinition/UKCore-Appointment"
		]
	},
	"status": "entered-in-error",
    "slot": [
        {
            "reference": "urn:uuid:deb4c4b3-870b-4599-84df-5e54cef7afda"
        }
    ],
	"description": "Reason for calling",
	"start": "2024-02-12T12:30:30+00:00",
	"end": "2024-02-12T12:40:30+00:00",
	"created": "2024-10-08T15:01:30+00:00",
	"participant": [
		{
			"actor": {
				"reference": "urn:uuid:788660eb-d2c9-4773-abd4-318484673fb2"
			},
			"status": "accepted"
		}
	]
}
```

<img src="https://raw.githubusercontent.com/NHSDigital/booking-and-referral-media/master/src/images/SequenceDiagrams/BaRS_Foundation_Cancel.drawio.svg" ></img>
