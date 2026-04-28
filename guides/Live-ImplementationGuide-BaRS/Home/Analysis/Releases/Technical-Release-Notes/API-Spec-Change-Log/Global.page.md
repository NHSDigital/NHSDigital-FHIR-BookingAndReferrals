---
topic: TRN-API-global
---

## {{page-title}}

### Change Log

| Change                                         | BaRS Version | Description                                                                                                                              | Impact                                                   |
|------------------------------------------------|--------------|------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------|
| <div class="imgHandshake">{{render:handshake}}</div> - Additional patient demographic parameters added to GET /Appointment | 1.9.0      | Patient demographic parameters (Name, Date of Birth and Address) added to support patient lookup for cancellation and update workflows.  | <mark style="background-color: Green">Addition</mark>    |
| <div class="imgHandshake">{{render:handshake}}</div> - Additional patient demographic parameters added to GET /ServiceRequest | 1.9.0      | Patient demographic parameters (Name, Date of Birth and Address) added to support patient lookup for cancellation and update workflows.  | <mark style="background-color: Green">Addition</mark>    |
| Fixed incorrect character display on GET /Slot description | 1.9.0      | Character display for a double quote was illegible.   | <mark style="background-color: Yellow">correction</mark>   |
|  Removal of use-context HTTP header  | 1.8.2   |Restricted the use of the use-context header to non-write operations  | <mark style="background-color: Yellow">correction</mark>  |
|  Improvments to header documentation   | 1.8.2   |Added better explanations for most of the headers needed  | <mark style="background-color: Green">Addition</mark> |
|  Addition of the use-context HTTP header  | 1.8.1   | A new header to assist in {{pagelink:core-EndToEndWorkflow-Logging-1.0.5, text: audting and logging}}  | <mark style="background-color: Green">Addition</mark> |
| <div class="imgHandshake">{{render:handshake}}</div> -  The DoS ID examples updated to https| 1.8.0      | The https://fhir.nhs.uk/Id/dos-service-id examples now correcly show as https.  | <mark style="background-color: Yellow">correction</mark>    |
| <div class="imgHandshake">{{render:handshake}}</div>  | 1.8.0 | The example deviceName element in NHSD-Requesting-Software now shows correctly as an Object as defined by the schema | <mark style="background-color: Yellow">correction</mark>    |
| Resilience to Endpoint Catalogue               | 1.5.0        | The proxies mechanism for obtaining Target Endpoints has been updated to allow for more resilience in the event of a dependency failure. | <mark style="background-color: Yellow">correction</mark> |
| Modifications to allow for future enhancements | 1.5.0        | The proxy has been modified to allow further endpoints and resources more easily in the future.                                          | <mark style="background-color: Yellow">correction</mark> |
| Publication of the 1.2.0 Specification         | 1.5.0        | 1.2.0 Specification (alpha) launched                                                                                                     | <mark style="background-color: Green">Addition</mark>    |
| Improvement to DocumentReference Schema   | 1.5.0 | the DocumentReference Schemas have been flattend for easier consumption | <mark style="background-color: Yellow">correction</mark>    |
| <div class="imgHandshake">{{render:handshake}}</div> - Corrections to example references containing http.  | 1.5.0 | Several references to http://fhir.nhs.uk have been corrected to "https". | <mark style="background-color: Yellow">correction</mark>    |

### Previous Releases