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

Request Body

```json
{
	"resourceType": "Appointment",
    "id":"1ed510f2-df15-45b7-8852-8adfb0fcf4f3",
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
	],
    "replaces": [
		{
			"reference": "Appointment/aca94bdb-2e38-4399-9ece-2ba083ce65b5"
		}		
	]
}
```

<img src="https://raw.githubusercontent.com/NHSDigital/NHSDigital-FHIR-BookingAndReferrals/main/BaRS-Images/SequenceDiagrams/BaRS_Foundation_ReBook.drawio.svg" ></img>

Once the appointment is rebooked, the Receiver is responsible for managing the pointer in the central Registry, as described in {{pagelink:core-StandardPattern-document-reference-1.3.1, text: Document Reference Standard Pattern }}.
