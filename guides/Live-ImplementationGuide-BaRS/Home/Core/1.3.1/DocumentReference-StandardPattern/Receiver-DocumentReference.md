---
topic: core-StandardPattern-document-reference-Receiver-1.3.1
---

# {{page-title}}

## Creating a DocumentReference.

The FHIR DocumentReference resource allows you to create a reference to a clinical document or resource. This section describes the process of creating a FHIR DocumentReference (pointer) for a booking or referral resource on the central Registry. A DocumentReference will be created when a Receiver accepts a booking or referral. Each booking or referral request processed requires a distinct DocumentReference on the Registry.


### Step 1: Identify the booking or referral to create a pointer for
When a Receiver processes a request for a booking (Appointment) or referral (ServiceRequest), the next step in the workflow is to create a pointer for the newly created resource (Appointment or ServiceRequest) on the central Registry. This will be undertaken via a POST [DocumentReference](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1.3.0#post-/DocumentReference) request to the BaRS Proxy.


### Step 2: Set content of the DocumentReference (pointer)
Create a new instance of the DocumentReference resource and populate the relevant fields. Key fields to include are as follows:

**identifier:** The DocumentReference needs several identifiers which allow the booking or referral to be located at a Receiver service.

The resource .id of the booking (Appointment) or referral (ServiceRequest) (created by the Receiver when processing the request) must be set in the 'value' element of an Identifier, clarified by the system '*https://fhir.nhs.uk/Id/BaRS-Identifier*'. 

```json
"identifier": [
	{
		"system": "https://fhir.nhs.uk/Id/BaRS-Identifier",
		"value": "8c63d621-4d86-4f57-8699-e8e22d49935d"
	}
```

The second identifier of note is the Receiving service who own the resource. The 'system' indicates the Service Discovery tool and the 'value', the identifier. In the code snippet below, the system '*https://fhir.nhs.uk/Id/dos-service-id*' indicates the Receiver service is on the Urgent and Emergency Care Directory of Services (UEC DoS) as service 2000072491. The Sender of any request will use the 'system' and 'value' here to build the base64 encoded HTTP Header NHSD-Target-Identifier, as defined for the [booking](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1.3.0#get-/Appointment/-id-) or [referral](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1.3.0#get-/ServiceRequest/-id-). 

```json
"identifier": [
	{
		"system": "https://fhir.nhs.uk/Id/dos-service-id",
		"value": "2000072491"
	}
```

The third identifier (currently optional) relates to the product-id, system '*https://fhir.nhs.uk/id/product-id*'. This is forthcoming functionality and further detail on its utility will follow but [working documentation] (https://github.com/NHSDigital/nhse-epr-integration/blob/main/pages/appendix1.md) is being actively updated.

```json
"identifier": [
	{
		"system": "https://fhir.nhs.uk/Id/product-id",
		"value": "P.GH7-4TY"
	}
```

**type:**, within the DocumentReference resource, indicates whether the pointer is for a booking or referral. BaRS currently only supports bookings (749001000000101) and referrals (736253002), described using SNOMED codes. 

```json
"type": {
	"coding": [
		{
			"system": "https://snomed.info/ict",
			"code": "749001000000101"
		}
	]
}
```

**subject:** specifies the subject of the DocumentReference, which will be the patient associated with the Resource. The patient's NHS number must be used to identify them, as outlined below.

```json
"subject": {
	"identifier": {
		"system": "https://fhir.nhs.uk/Id/nhs-number",
		"value": "9556274839"
	}
},
```

**custodian:** Set the author of the DocumentReference, which will be the ODS code for the organisation writing the DocumentReference resource entry.

```json
	"custodian": {
		"identifier": {
			"system": "https://fhir.nhs.uk/Id/ods-organization-code",
			"value": "A1001"
		}
	}
```

**context:** MUST include a period set to the Appointment start and end times.

```json
"context": {
  "period": {
    "start": "2025-02-12T12:30:30+00:00",
    "end": "2025-02-12T12:40:30+00:00"
  }
}
```

### Step 3: Save and Transmit the DocumentReference (pointer)
Once all the necessary fields are populated, perform a [POST](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1.3.0#post-/DocumentReference) of the DocumentReference to the /DocumentReference endpoint on the BaRS proxy. This will create a DocumentReference in the NRL.

After saving, the DocumentReference will be assigned a unique id (e.g., DocumentReference/12345). This can be used to reference or [retrieve](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1.3.0#get-/DocumentReference/-id-) the DocumentReference in the future.

### Step 4: Verify the DocumentReference
To ensure that the DocumentReference was created successfully, retrieve it using its [id](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1.3.0#get-/DocumentReference/-id-) or [search](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1.3.0#get-/DocumentReference) for it using relevant parameters. Make sure to validate the returned DocumentReference to confirm that all the contents are accurate.

### Updating a DocumentReference
A DocumentReference can be updated by performing a [PUT](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1.3.0#put-/DocumentReference/-id-) request with the updated resource to the /DocumentReference endpoint on the BaRS proxy with the appropriate DocumentReference.id. A Read operation must be performed prior to this to ensure that the new DocumentReference is the most up to date.

**Note**: A Receiver can only update DocumentReference resources that they created and own.

### Delete a DocumentReference
A DocumentReference can be removed by performing a [DELETE](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1.3.0#delete-/DocumentReference/-id-) request to the /DocumentReference endpoint on the BaRS proxy with the appropriate DocumentReference.id. A Read operation must be performed prior to this to ensure that the action is appropriate.

**Note**: A Receiver can only delete DocumentReference resources they created and own.

<a href="https://raw.githubusercontent.com/NHSDigital/NHSDigital-FHIR-BookingAndReferrals/main/BaRS-Images/DocumentReference/BaRS_NRL_Write_Sequence-1.1.0.svg" target="_blank">
<img src="https://raw.githubusercontent.com/NHSDigital/NHSDigital-FHIR-BookingAndReferrals/main/BaRS-Images/DocumentReference/BaRS_NRL_Write_Sequence-1.1.0.svg" ></img></a>

.