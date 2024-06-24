---
topic: core-Security-Auth-1.1.3
---

## Authorisation

BaRS will use several HTTP headers to facilitate authorisation. Although optional, receivers can expect these to be present for each request (excluding /metadata and /MessageDefinition), where applicable, to enforce access control. These will be in addition to the X-Request-ID and the X-Correlation-ID headers. If the information in these headers is available in the sending system, they'll be included in the request.

Each of these HTTP headers are objects and will therefore need to be added in the form of a standard Base64 encoded string.

Examples of each HTTP header item can be found within the [API Specification](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir).

| HTTP Header                  | Purpose                                                                                                                                                                                                                  |
|------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| NHSD-End-User-Organisation   | This will represent the organisation making the request. It Shall include the ODS code and the human readable name of the organisation making the request. The object is based on a FHIR Organisation resource.          |                                                                                                                             |
| NHSD-Requesting-Practitioner | This entry will represent the Practitioner role associated to the request. It shall include their sds role id and a SNOMED code related to their role where applicable.  The object is based on a FHIR PractitionerRole resource. |
| NHSD-Requesting-Software     | This entry will represent the Software or application making the request. It shall include an identifier for the instance, the product name and its version. The object is based on a FHIR Device resource.              |