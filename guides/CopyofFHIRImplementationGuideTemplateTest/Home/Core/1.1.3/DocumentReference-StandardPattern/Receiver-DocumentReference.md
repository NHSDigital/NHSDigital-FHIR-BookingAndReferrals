---
topic: core-StandardPattern-document-reference-Receiver-1.1.3
---

# {{page-title}}

## Creating a DocumentReference.

The FHIR DocumentReference resource allows you to create a reference to a clinical document or resource. This section describes the process of creating a FHIR DocumentReference for a resource. A DocumentReference will be created when a Receiver accepts a Booking or a Referral. Each request will warrant a distinct Document Reference.

### Step 1: Understand the Document Reference Resource
The Document Reference resource in FHIR represents a reference to a clinical document or resource. It contains metadata about the document, such as its type, author, and creation date, along with a reference to the actual document's location. Within BaRS the DocumentReference acts as a pointer towards ServiceRequests, or Appointment resources.

### Step 2: Identify the Resource to Reference
Determine the resource that you want to create a Document Reference for. This will be any ServiceRequest or Appointment Resource that has been created in the Receiver system by means of a booking request or a service request.

The resources themselves will have unique identifiers upon creation in the receiver system.

### Step 3: Set the Metadata of the Document Reference
Create a new instance of the Document Reference resource and populate the relevant metadata fields. key fields to include are as follows:

type: Specify the type of document or resource being referenced. For example, if you are referencing a referral you would use the value `https://snomed.info/ict|736253002` or if it is a booking `https://snomed.info/ict|749001000000101`.

```json
"type": {
	"coding": [
		{
			"system": "https://snomed.info/ict",
			"code": "736253002"
		}
	]
}
```

subject: Specify the subject of the document reference, which is typically the patient associated with the Resource.
```json
"subject": {
	"identifier": {
		"system": "https://fhir.nhs.uk/Id/nhs-number",
		"value": "9556274839"
	}
},
```

custodian: Set the author of the document reference, which will be the ODS code for the organisation writing the DocumentReference.
```json
	"custodian": {
		"identifier": {
			"system": "https://fhir.nhs.uk/Id/ods-organization-code",
			"value": "A1001"
		}
	}
```


### Step 4: Set the Content Reference
The content element of the Document Reference resource contains the reference to the location of the actual resource. Create a new instance of the content element and set the attachment property. The attachment property has a URL field where you specify the location of the resource.

Access the content element of the Document Reference. This element contains the reference to the location of the actual resource. The content element is typically an array, as a DocumentReference can reference multiple versions or representations of the same document. Each item in the array will have a URL element, which specifies the location of the resource.

The content.attachment.URL element in this example is a URL friendly Target Identifier for the receiver endpoint, of which can be used to retrieve the resource via the BaRS proxy by a consumer/sender. This element can also contain a direct URL if appropriate.
The content.format element will contain the coding that describes the format of the resource in question. In this instance this is a [BaRS message event](https://simplifier.net/nhsbookingandreferrals/message-events-bars) of "servicerequest-request". ensure you set the creation date of the resource.

```json
"content": [
	{
		"attachment": {
			"language": "en-UK",
			"URL": "http://fhir.nhs.uk/Id/dos-service-id|111111111",
			"title": "Physical",
			"creation": "2005-12-24T09:35:00+11:00"
		},
		"format": [
			{
				"coding": [
					{
						"system": "https://fhir.nhs.uk/CodeSystem/message-events-bars",
						"code": "servicerequest-request"
					}
				]
			}
		]
	}
]
```
### Step 5: Save and Transmit the DocumentReference
Once you have populated all the necessary fields, you will need to perform a POST of the DocumentResource to the /DocumentReference endpoint on the BaRS proxy. This will create a DocumentReference in the NRL.

After saving, the DocumentReference will be assigned a unique id (e.g., DocumentReference/12345). You can use this identifier to reference or retrieve the DocumentReference in the future.

### Step 6: Verify the DocumentReference
To ensure that the DocumentReference was created successfully, you can retrieve it using its identifier or search for it using relevant parameters. Make sure to validate the returned DocumentReference to confirm that all the metadata and content references are accurate.

### Updating a DocumentReference
A DocumentReference can be updated by performing a PUT request with the updated resource to the /DocumentReference endpoint on the BaRS proxy with the appropriate id. A Read operation must be performed prior to this to ensure that the new DocumentReference is the most up to date.

**Note**: You can only delete DocumentReference resources that you own and that you created.

### Delete a DocumentReference
A DocumentReference can be updated by performing a DELETE request with the resource to the /DocumentReference endpoint on the BaRS proxy with the appropriate id. A Read operation must be performed prior to this to ensure that the Action is appropriate.

**Note**: You can only delete DocumentReference resources that you own and that you created.

<a href="https://raw.githubusercontent.com/NHSDigital/booking-and-referral-media/master/src/images/DocumentReference/BaRS_NRL_Write_Sequence-1.1.0.svg" target="_blank">
<img src="https://raw.githubusercontent.com/NHSDigital/booking-and-referral-media/master/src/images/DocumentReference/BaRS_NRL_Write_Sequence-1.1.0.svg" ></img>

