---
topic: TRN-API-global
---

## {{page-title}}

### Change Log

| Change                                         | BaRS Version | Description                                                                                                                              | Impact                                                   |
|------------------------------------------------|--------------|------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------|
|  Addition of the use-context HTTP header  | 1.8.1   | A new header to assist in {{pagelink:core-EndToEndWorkflow-Logging-1.0.5, text: audting and logging}}  | <mark style="background-color: Green">Addition</mark> |
| <div class="imgHandshake">{{render:handshake}}</div> -  The DoS ID examples updated to https| 1.8.0      | The https://fhir.nhs.uk/Id/dos-service-id examples now correcly show as https.  | <mark style="background-color: Yellow">correction</mark>    |
| <div class="imgHandshake">{{render:handshake}}</div>  | 1.8.0 | The example deviceName element in NHSD-Requesting-Software now shows correctly as an Object as defined by the schema | <mark style="background-color: Yellow">correction</mark>    |
| Resilience to Endpoint Catalogue               | 1.5.0        | The proxies mechanism for obtaining Target Endpoints has been updated to allow for more resilience in the event of a dependency failure. | <mark style="background-color: Yellow">correction</mark> |
| Modifications to allow for future enhancements | 1.5.0        | The proxy has been modified to allow further endpoints and resources more easily in the future.                                          | <mark style="background-color: Yellow">correction</mark> |
| Publication of the 1.2.0 Specification         | 1.5.0        | 1.2.0 Specification (alpha) launched                                                                                                     | <mark style="background-color: Green">Addition</mark>    |
| Improvement to DocumentReference Schema   | 1.5.0 | the DocumentReference Schemas have been flattend for easier consumption | <mark style="background-color: Yellow">correction</mark>    |
| <div class="imgHandshake">{{render:handshake}}</div> - Corrections to example references containing http.  | 1.5.0 | Several references to http://fhir.nhs.uk have been corrected to "https". | <mark style="background-color: Yellow">correction</mark>    |

This Section will list all updates to the BaRS API Specification within the 1.2.0 minor release, published for BaRS 1.5.0.

### Publication of the 1.2.0 API Specification (in development)

The API Spec landing page will now have the an additional version to select to view. At present this will present 1.0.0, 1.1.0 and 1.2.0, with links to each specification. 1.1 and 1.2.0 are currently in development.

### Endpoint Catalogue

**EndpointCatalogue related Endpoints have been added to the specification in preparation for future use cases.** 

The following endpoints are now available in the 1.2.0 specification. These endpoints will be used in future use cases and future iterations of current use cases.

* GET /Endpoint
* GET /HealthcareService
* GET /Organization
* GET /Endpoint/[id]
* GET /HealthcareService/[id]
* GET /Organization/[id]
* PUT /Endpoint/[id]
* PUT /HealthcareService/[id]
* PUT /Organization/[id]
* DELETE /Endpoint/[id]
* DELETE /HealthcareService/[id]
* DELETE /Organization/[id]

### Appointment

The following endpoints have been provisionally added to the 1.2.0 specification. These endpoints will be used in future use cases and future iterations of current use cases.

* POST /Appointment/[id]
* PUT /Appointment/[id]
* PATCH /Appointment/[id]
* DELETE /Appointment/[id]

### ServiceRequest

The following endpoints have been provisionally added to the 1.2.0 specification. These endpoints will be used in future use cases and future iterations of current use cases.

* POST /Appointment/[id]
* PUT /Appointment/[id]
* PATCH /Appointment/[id]
* DELETE /Appointment/[id]
