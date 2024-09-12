
{{tree:https://hl7.org/fhir/R4/StructureDefinition/Flag , hybrid}}

# BaRS API Spec Change Log for v1.0.0
## 2023 Post FOT for exiting private beta
| Owner          | Status      |
|----------------|-------------|
| Leigh Goslin | In Progress |

## General

**The API Spec Version has been uplifted to 1.0.0**

**Broken links to the BaRS Standard documentation have been rectified.**

**BaRS Proxy production URL has been added to the [Environments and Testing](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir#api-description__environments-and-testing) section.**

**The [Error Handling](https://simplifier.net/guide/nhsbookingandreferralstandard/home/design/design--core#Error-handling) link now correctly refers to the BaRS Core [implementation guidance](https://simplifier.net/guide/nhsbookingandreferralstandard/home/design/design--core#Error-handling).**

**Broken links within the Specifications schema examples have been rectified.**

**Examples included within the Specifications files have been updated for clarity.**

**Examples referenced by the Specification have been updated for clarity.****

## Headers

**The Accept Header must now include a version. The version is mandatory, the specification now shows the Accept header as mandatory to reflect this.** 

```bash
 --header 'Accept: application/fhir+json; version=1.0.0-beta'
```



**The following Access Control headers have been made mandatory where they are currently included.**

* NHSD-End-User-Organisation (Required)
* NHSD-Requesting-Software (Required)

**The following Access Control headers have been reintroduced to the GET /metadata and GET /MessageDefinition endpoints. For consistency, the mandated items match other endpoints.**

* NHSD-End-User-Organisation (Required)
* NHSD-Requesting-Software (Required)
* NHSD-Requesting-Practitioner

## Parameters

**The following parameter has been added to the GET /ServiceRequest endpoint to support searching by identifiers.**

* ServiceRequest.identifier
    * This will be a unique booking reference number/identifier of a referral, or a unique UUID/GUID for the referral. This is not the same as the ServiceRequest.id



**The context paramater for GET /MessageDefinition now requires a system|value format, as opposed to a value.**

     http://fhir.nhs.uk/Id/dos-service-id|2000099999

## Guidance and QOL
**The descriptions and guidance for all Access Control headers have been expanded.**
* NHSD-End-User-Organisation (Required)
* NHSD-Requesting-Software (Required)
* NHSD-Requesting-Practitioner

**The description and guidance for _include paramaters on GET /Slot has been expanded.**
* expressions have been added for clarity.
* minimum usage guidance added.

**The description and guidance for GET /metadata has been expanded.**
* usage and expected content has been added.
* guidance on obtaining the BaRS Proxy CapabilityStatement has been Added.

**Identified typos and spelling mistakes have been corrected.**