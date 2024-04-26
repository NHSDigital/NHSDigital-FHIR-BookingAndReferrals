---
topic: core-foundation-appointment-rebook-1.1.3
---

### Rebook

Notes on Rebook from https://hl7.org/fhir/R4/appointment.html

#### Waitlisting the Appointment (optional)

This optional step permits creating a waitlisted appointment. This could occur if an appointment needs to be booked into a time that is not ideal for the patient due to lack of available time slots. In this workflow, there would be two appointments, the booked appointment in the time slot that is currently available, and the waitlisted appointment with a requestedPeriod spanning the time that the patient would prefer if new slots become available.

If new time slots become available during the requestedPeriod, the scheduling system, or staff at the scheduling organization, can notify the patient that a new time slot is available. If the patient chooses, the waitlisted appointment would then be booked into that specific slot, and the previously booked appointment would be cancelled. The specific business process for notifying patients of new availability is not specified, and is up to the implementing system to determine.

under section 12.10.4.5 Flow for a patient waitlist: 

| Activity Description                                                                 | Appointment (inconvenient)                              | Appointment (preferred)                                                              |
|--------------------------------------------------------------------------------------|---------------------------------------------------------|--------------------------------------------------------------------------------------|
| An appointment is booked for an inconvenient time using a typical status flow | status = bookedparticipant.status = accepted |                                                                                      |
| Waitlist appointment created                                                  | status = bookedparticipant.status = accepted | status = waitlistrequestedPeriod = (more convenient time period) |
| Patient notified of availability of a better slot                             | status = booked                                  | status = proposedparticipant.status = needs-action                        |
| Patient accepts better slot                                                   | status = cancelled                               | status = bookedparticipant.status = accepted                              |

The FHIR guidance indicates that the Appointment that is no longer needed should be updated with a PUT status=cancelled

A new Appointment can then be created as needed using the same existing workflow, whether this is using the Slot/Schedule or a POST Appointment resource.
Use the cancel method described above.

#### Process for rebook
The method for the subsequent booking of an appointment depends on the Application specific guidance within BaRS. The only difference would be the Appointment Resource would include Appointment.replaces referencing the previous appointment for provenance.

Using PUT:

* Select the service to book an appointment with. 
* Confirm BaRS Capabilities.
* Request Available slots.
* Select a slot.
* Perform a GET operation using the id of the appointment to /Appointment[id]
* Set the Appointment.status value to "cancelled"
* Perform a PUT operation using the id of the appointment to /Appointment[id]

Request Body

```json
{
	"resourceType": "Appointment",
    "id":"1ed510f2-df15-45b7-8852-8adfb0fcf4f3"
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
	],
    "replaces": [
		{
			"reference": "urn:uuid:aca94bdb-2e38-4399-9ece-2ba083ce65b5"
		}		
	]
}
```

Using PATCH:

* Select the service to book an appointment with. 
* Confirm BaRS Capabilities.
* Request Available slots.
* Select a slot.
* Perform a GET operation using the id of the appointment to /Appointment[id]
* Set the Appointment.status value to "cancelled"
* Perform a PATCH operation using the id of the appointment to /Appointment[id]

```json
{
	"resourceType": "Appointment",
    "id":"1ed510f2-df15-45b7-8852-8adfb0fcf4f3",
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
}
```

<img src="https://raw.githubusercontent.com/NHSDigital/booking-and-referral-media/master/src/images/SequenceDiagrams/BaRS_Foundation_ReBook.drawio.svg" ></img>
