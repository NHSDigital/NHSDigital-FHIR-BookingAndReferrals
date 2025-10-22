---
topic: core-StandardPattern-document-reference-Sender-1.3.1
---

# {{page-title}}

### Step 1: Understand the Document Reference Resource
The FHIR DocumentReference resource represents a reference to a clinical document or resource, in the case of BaRS a pointer to an active booking or referral. It contains metadata about the booking or referral, such as its type (booking or referral), author, and subject (the patient's NHS number), as well as a reference to the actual document's .id and where it resides (the service who owns it); the two key data points needed to retrieve it. 

### Step 2: Search for the booking or referral pointer (DocumentReference)
FHIR DocumentReference resources holding pointers for BaRS bookings and referrals are stored in a central Registry, within NRL (National Record Locator), as decribed above, and interrogated through the [BaRS API DocumentReference](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1.3.0#get-/DocumentReference).

To find a booking or referral location, you need to search for the appropriate DocumentReference resource from the Registry, using search parameters. It is mandatory to include the subject:identifier (the patient's NHS number), other parameters can be used to filter the response further e.g type of document (booking and referral). 

### Step 3: Inspect the booking or referral pointer (DocumentReference)
Once you retrieve the Document Reference(s) (pointers) from the search, inspect the returned resources to identify the one you need. Look for relevant metadata, as described below, to confirm the correct resource.

**identifier:** The DocumentReference will have several identifiers which are required to locate the booking or referral at a Receiver service.

The .id of the booking or referral is indicated by the system '*https://fhir.nhs.uk/Id/BaRS-Identifier*'. The value can be used to directly request the [booking](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1.3.0#get-/Appointment/-id-) or [referral](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1.3.0#get-/ServiceRequest/-id-) by .id, once you know Receiver service holding it (see next identifier).

```json
"identifier": [
	{
		"system": "https://fhir.nhs.uk/Id/BaRS-Identifier",
		"value": "8c63d621-4d86-4f57-8699-e8e22d49935d"
	}
```

The second identifier, required to make the subsequent request for the booking or referral in question, has a system of '*https://fhir.nhs.uk/Id/dos-service-id*' and enables the Sender to direct their request to the Receiver service which owns it. The Sender will use the system and value here to build the base64 encoded HTTP Header NHSD-Target-Identifier, as defined for the [booking](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1.3.0#get-/Appointment/-id-) or [referral](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1.3.0#get-/ServiceRequest/-id-).

```json
"identifier": [
	{
		"system": "https://fhir.nhs.uk/Id/dos-service-id",
		"value": "2000072491"
	}
```

The third identifier (currently optional) relates to the product-id, system '*https://fhir.nhs.uk/id/product-id*'. This is forth coming functionality and further detail on its utility will follow but [working documentation] (https://github.com/NHSDigital/nhse-epr-integration/blob/main/pages/appendix1.md) is being actively updated.

```json
"identifier": [
	{
		"system": "https://fhir.nhs.uk/Id/product-id",
		"value": "P.GH7-4TY"
	}
```

**type:** within the DocumentReference Resource, indicates whether the pointer is for a booking or referral. BaRS currently only supports bookings (749001000000101) and referrals (736253002), described using SNOMED codes. This information is required to direct the subsequent request to the correct endpoint for the [booking](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1.3.0#get-/Appointment/-id-) or [referral](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1.3.0#get-/ServiceRequest/-id-)

```json
"type": {
	"coding": [
		{
			"system": "https://snomed.info/ict",
			"code": "749001000000101",
			"display": "Appointment (record artifact)"
		}
	]
}
```

**subject:** The subject will describe the patient, by means of an NHS number. This element is not explicitly required to request the specific resource dictated by the pointer but could be used to search a service more widely for related [bookings](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1.3.0#get-/Appointment) and [referrals](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1.3.0#get-/ServiceRequest), using the search by patient endpoints. 

```json
"subject": {
	"identifier": {
		"system": "https://fhir.nhs.uk/Id/nhs-number",
		"value": "9556274839"
	}
```

**custodian:** The custodian element will describe the organisation that owns the resource data. This will be a concatenation of ODS codes. 

```json
	"custodian": {
		"identifier": {
			"system": "https://fhir.nhs.uk/Id/ods-organization-code",
			"value": "A1001"
		}
	}
```

**context:** includes a period set to the Appointment start and end times.

```json
"context": {
  "period": {
    "start": "2025-02-12T12:30:30+00:00",
    "end": "2025-02-12T12:40:30+00:00"
  }
}
```

### Step 4: Retrieve the booking or referral
The booking or referral resource can be retrieved by making a GET request for the [booking](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1.3.0#get-/Appointment/-id-) or [referral](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1.3.0#get-/ServiceRequest/-id-). 

The two key values required to make the request are the first two identifiers in the DocumentReference;  the resource .id ('*https://fhir.nhs.uk/Id/BaRS-Identifier*') and service id ('*https://fhir.nhs.uk/Id/dos-service-id*'). Use the resource .id populate the location of the request and service id to populate the NHSD-Target-Identifier HTTP Header, as described in the worked example below.  

For BaRS, a GET of the relevant resource using the Target Identifiers. In this simplified example, the identifier containing the service id is used in the NHSD-Target-Identifier header, instructing the BaRS proxy to route to the request to that target  **note**: The header is not base64Encoded in this example:

```
cURL --location 'https://int.api.service.nhs.uk/booking-and-referral/FHIR/R4/Appointment/8c63d621-4d86-4f57-8699-e8e22d49935d' \
--header 'X-Request-ID: {{X-Request-ID}}' \
--header 'X-Correlation-ID: {{X-Correlation-ID}}' \
--header 'NHSD-Target-Identifier: {system:"http://fhir.nhs.uk/Id/dos-service-id", value:"111111111"}' \
--header 'Accept: application/fhir+json' \
```

### Step 5: Handle the Retrieved booking or referral
Once you have retrieved the booking or referral resource, it can be used in subsequent workflows. Refer to the FHIR documentation or resource-specific or application-specific guides for further information on handling the retrieved resource.

**Note**: It's important to consider the security and privacy aspects when working with clinical documents and resources. Ensure that you adhere to applicable regulations and best practices to protect patient data.

<a href="https://raw.githubusercontent.com/NHSDigital/NHSDigital-FHIR-BookingAndReferrals/main/BaRS-Images/DocumentReference/BaRS_NRL_Search_Sequence-1.1.0.svg" target="_blank">
<img src="https://raw.githubusercontent.com/NHSDigital/NHSDigital-FHIR-BookingAndReferrals/main/BaRS-Images/DocumentReference/BaRS_NRL_Search_Sequence-1.1.0.svg" ></img></a>

.

