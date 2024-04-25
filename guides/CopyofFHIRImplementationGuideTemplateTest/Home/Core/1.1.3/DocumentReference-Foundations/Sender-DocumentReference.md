---
topic: core-document-reference-Sender-1.1.3
---

# {{page-title}}

### Step 1: Understand the Document Reference Resource
The Document Reference resource in FHIR represents a reference to a clinical document or resource. It contains metadata about the document, such as its type, author, and creation date, subject (the patients NHS number), as well as a reference to the actual document's location (URL) and markers for how the method needed to retrieve it. 

### Step 2: Search for the Document Reference
To find a resource's location, you need to search for the appropriate DocumentReference resource. The most common way to search for Document References is by using search parameters.

For example, if you are looking for a DocumentReference that represents a referral, you could use the following search query, where a snomed code is used to define the type of the document:

GET [base-URL]/DocumentReference?type=https://snomed.info/ict|736253002

The Booking and Referrals API [v1.1.0 specification](google.com) has more information on search parameters available.

### Step 3: Inspect the Document Reference
Once you retrieve the Document Reference(s) from the search, inspect the returned resources to identify the one you need. Look for relevant metadata like the document type, author, creation date or format to confirm it is the correct resource.

identifier: The DocumentReference will have an identifier stating the id of the resource.
```
"identifier": [
	{
		"system": "https://fhir.nhs.uk/Id/BaRS-Identifier",
		"value": "8c63d621-4d86-4f57-8699-e8e22d49935d"
	}
```

type: Below you can see the type, within the DocumentReference Resource. Within BaRS there is currently only bookings (749001000000101) and Referrals (736253002), described using SNOMED codes.
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

subject: The subject will describe the patient, by means of an NHS number.

```json
"subject": {
	"identifier": {
		"system": "https://fhir.nhs.uk/Id/nhs-number",
		"value": "9556274839"
	}
```

custodian: The custodian element will describe the organization that owns the resource data. This will be a concatenation of ODS codes. 

```json
	"custodian": {
		"identifier": {
			"system": "https://fhir.nhs.uk/Id/ods-organization-code",
			"value": "A1001"
		}
	}
```
### Step 4: Retrieve the Resource's Location
Access the content element of the Document Reference. This element contains the reference to the location of the actual resource. The content element is typically an array, as a Document Reference can reference multiple versions or representations of the same document. Each item in the array will have a URL element, which specifies the location of the resource.

The content.attachment.URL element in this example is a URL friendly Target Identifier, of which can be used to retrieve the resource. This element can also contain a direct URL if appropriate.
The content.format element will contain the coding that describes the format of the resource in question. In this instance this is a [BaRS message event](https://simplifier.net/nhsbookingandreferrals/message-events-bars) of "servicerequest-request".

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
### Step 5: Retrieve the Resource
Retrieve the resource by making a GET request to the URL specified in the URL element of the Document Reference's content. Ensure that you have the necessary authorization and access privileges to retrieve the resource.

For BaRS, a GET of the relevant resource type using the Target Identifiers. In this simplified example the URL above containing a TargetIdentifier is used in the NHSD-Target-Identifier header to instruct the BaRS proxy to route to the request to that target  **note**: The header is not base64Encoded in this example:

``` bash
cURL --location 'https://int.api.service.nhs.uk/booking-and-referral/FHIR/R4/ServiceRequest/8c63d621-4d86-4f57-8699-e8e22d49935d' \
--header 'X-Request-ID: {{X-Request-ID}}' \
--header 'X-Correlation-ID: {{X-Correlation-ID}}' \
--header 'NHSD-Target-Identifier: {system:"http://fhir.nhs.uk/Id/dos-service-id", value:"111111111"}' \
--header 'Accept: application/fhir+json' \
```

Also, if the content element has a direct URL, this can be obtained using a direct GET request.

### Step 6: Handle the Retrieved Resource
Once you have retrieved the resource, you can process it according to your requirements. The format and structure of the resource will depend on the specific resource type, such as Patient or ServiceRequest. Refer to the FHIR documentation or resource-specific or application-specific guides for further information on handling the retrieved resource.

**Note**: It's important to consider the security and privacy aspects when working with clinical documents and resources. Ensure that you adhere to applicable regulations and best practices to protect patient data.

<a href="https://raw.githubusercontent.com/NHSDigital/booking-and-referral-media/master/src/images/DocumentReference/BaRS_NRL_Search_Sequence-1.1.0.svg" target="_blank">
<img src="https://raw.githubusercontent.com/NHSDigital/booking-and-referral-media/master/src/images/DocumentReference/BaRS_NRL_Search_Sequence-1.1.0.svg" ></img>

