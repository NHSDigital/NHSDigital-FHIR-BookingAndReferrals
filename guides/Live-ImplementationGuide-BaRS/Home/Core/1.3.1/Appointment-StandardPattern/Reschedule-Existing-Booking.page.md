---
topic: core-StandardPattern-appointment-reschedule-1.3.1
---

### Reschedule 

The Reschedule operation supports amending the slot a booking is made against. The slot is the only element capable of being changed as part of the reschedule operation, if either the .status or .reasonCode require amendment, the {{pagelink:core-StandardPattern-appointment-update-1.3.1, text:Update}} operation can be followed, otherwise, the {{pagelink:core-StandardPattern-appointment-rebook-1.3.1, text:Rebook}} operation.

Steps to Reschedule:

* Perform a [GET](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1.3.0#get-/Appointment/-id-) operation using the .id of the appointment to /Appointment/\{id\}. Alternatively, if the .id is not known, a search of the Registry can be undertaken following the {{pagelink:core-StandardPattern-document-reference-Sender-1.3.1, text: Document Reference Standard Pattern - Sender}}. NB: If a match cannot be obtained using this method the process of updating must be performed manually
* [Request Available slots](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1.3.0#get-/Slot) from the service
* Select a new slot
* Update the resource with the new slot. NB: Only the .slot element of the resource must be updated
* Perform a [PATCH](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1.3.0#patch-/Appointment/-id-) operation using the id of the appointment to /Appointment/\{id\}
* Once processed, the Receiver of the booking must [update (PUT)](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1.3.0#put-/DocumentReference/-id-) the pointer in the central Registry, as described in {{pagelink:core-StandardPattern-document-reference-Receiver-1.3.1, text: Document Reference Standard Pattern - Receiver}}. The principle update to the pointer is to change the .context element to alter the slot time - 

```json
"context": {
  "period": {
    "start": "2025-02-12T12:30:30+00:00",
    "end": "2025-02-12T12:40:30+00:00"
  }
}
```


In this example the Appointment resource is with the existing slot, and updated with the newly selected slot. 

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
    "slot": [
        {
            "reference": "Slot/265a53d7-1d21-4fc6-a5b7-761f650e75eb"
        }
    ],
	"description": "Reason for calling",
	"start": "2025-02-12T10:00:30+00:00",
	"end": "2025-02-12T10:10:30+00:00",
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
	"start": "2025-02-12T12:30:30+00:00",
	"end": "2025-02-12T12:40:30+00:00",
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
<img src="https://raw.githubusercontent.com/NHSDigital/NHSDigital-FHIR-BookingAndReferrals/main/BaRS-Images/SequenceDiagrams/BaRS_Foundation_Reschedule.drawio.svg" ></img>
