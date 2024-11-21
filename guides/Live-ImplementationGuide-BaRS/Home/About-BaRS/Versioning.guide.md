---
topic: version-negotiation
---

## Versioning
The Booking and Referral Standard (BaRS) will follow [Semantic Versioning](https://semver.org/), i.e. a three-part version number consisting of major, minor and patch versions.  There will also be support for pre-releases versioning by use of ALPHA and BETA extensions

Full details can be found at the [Semantic Versioning](https://semver.org/) site, key points outlined below:

#### Major version
The major version is incremented when an incompatible changes are made, i.e. a non backwards compatible change.

#### Minor version
The minor version increments when changes are made in a backwards compatible manner.

#### Patch version
The patch version is incremented when backwards compatible bug fixes are implemented.

#### Extensions
The extensions ALPHA, BETA or RC (Release Candidate) will be used to indicate the maturity of a pre-release version.


### Components  
An appreciation of the components involved in a released version must be understood when building solutions. These separate components come together under the umbrella of a given overall version but the components themselves are also versioned. This published implementation guide denotes the 'overall version' referenced. 

Components involved in an overall version:- 
* **{{pagelink:design-core-1.0.5, text:Core}}**: BaRS Core components - API Spec, Endpoint Catalogue etc.
* **[Package](https://simplifier.net/NHSBookingandReferrals/~packages)**: FHIR package
* **{{pagelink:applications, text:Application}}**: the use cases i.e. '111 to ED'
* **{{pagelink:fhir_assets, text:FHIR Assets}}**: MessageDefinitions and profiles

The following worked example will help further explain how components, their versions and the overall version correlate. 

The initial BaRS overall released version was **1.0.0-alpha**. This includes the API Spec, FHIR package, 111 to ED (Emergency Department(A&E)) bookings and referrals Application, 999 to CAS (Clinical Assessment Service) validation and referral Application, along with their related MessageDefinitions to support workflows. Suppliers can build any workflow i.e. 111 to ED booking and referral Sender and expect to be compatible with any other supplier who has built the corresponding (111 to ED booking and referral Receiver) workflow. Following a successful public beta period, version 1.0.0-alpha is incremented to 1.0.0.

In the example, hypothetically, a version 1.1.0 is created, due to subsequent revision of the 999 to CAS use case, requiring non-breaking changes to the API Spec and Message Definition. The non breaking changes could include optional HTTP headers on an endpoint or an optional resource being included in the Message Definition. This will mean changes to the overall version, API Spec, FHIR package and Message Definitions related to the 999 to CAS Application. However, backward compatibility is maintained because the changes are optional.

Breaking change will always be considered before being implemented, the overhead of introducing such changes to solutions already in Production is well appreciated. A breaking change will trigger a major version release, adhering to semantic versioning as described above. A breaking change could include a new API endpoint for a new BaRS Application or change to an existing Application workflow, mandated HTTP header value and/or additional mandated resources included in updated Message Definitions. 

### <span style="color:red">**For the Core elements of BaRS (BaRS Core) suppliers will be expected to revise their solution to support a MAJOR release within six months from the version release date**</span>

<span style="color:red">Note: Major releases of BaRS Core will be NO LESS than SIX MONTHS from the preceeding major release</span>


<center>
{{render:versioning.png}}
</center>

Compatibilty is verified dynamically during workflows through the 'version' element defined on the Capability Statement and Message Definitions. Senders and Receivers should operate on the highest version they are both compatible with and negoitate down, where possible. 

A Sender **must** check the returned 'version' in these resources before proceeding to make requests of a Receiver. For version 1.0.0 **only** versions within the major version v1.0.0 should be considered compatible (1.0.0 extensions excluded):-

<center>
{{render:CapabilityStatement.png}}
</center>

A Receiver **should** check the version a Sender is expecting interoperate on by checking the value included in the request via the HTTP Accept Header. For version 1.0.0 **only** versions within the major version v1.0.0  should be considered compatible (1.0.0 extensions excluded):-

<center>
{{render:AcceptHeader.png}}
</center>

### Pre-release Labels
These labels will be taken from the GDS (Goverment Digital Services) development process stages, and will be one of:

* **Discovery**: a Feasibility study. A 'No code' development. Designed to find out what users are trying to achieve, any constraints, improvement opportunities

* **Alpha**: Develop prototypes and test with users. Could be minimal functionality and potentially prototypes for any options to determine which is best

* **Private Beta**: Working version and test with invited users. Handle real transactions and work at scale. ‘Invite only’ or regional. Must Pass assessment by business and technical SME’s

* **Public Beta**: All users can participate. Version unlikely to change substantially, but still needs further testing by a wider group of implementors before becoming live

* **Live**: The live phase is about supporting the service in a sustainable way, and continuing to iterate and make improvements

* **Retiring**: Implementors notified that the service is discontinued and not to be used for new developments

<hr>

## Version Negotiation

The Booking and Referrals standard implements version negotiation in 3 steps. Each step is protected by the step before it. Version negotiation works in a similar way at each step. The 3 stages are the API version header, the call to GET /CapabilityStatement and the call to GET /MessageDefinition.

### API (step 1)

APIs should have the ability to route traffic based on the version header as shown below. This is to ensure that major version differences (breaking changes) can be negotiated as shown in the second diagram.


<a href="https://raw.githubusercontent.com/NHSDigital/NHSDigital-FHIR-BookingAndReferrals/main/BaRS-images/images//Versioning/API_Proxies-1.1.0.svg" target="_blank"><img src="https://raw.githubusercontent.com/NHSDigital/NHSDigital-FHIR-BookingAndReferrals/main/BaRS-images/images/Versioning/API_Proxies-1.1.0.svg" width="800"></img></a>

API Versioning between entities is fairly loose, only the major versioning differences would case a failure. with the exception of new endpoints which will be gated by minor versioning. The diagram below shows desired behavior in all versioning negotiations at the API.

<a href="https://raw.githubusercontent.com/NHSDigital/NHSDigital-FHIR-BookingAndReferrals/main/BaRS-images/images//Versioning/API_Interactions-1.1.0.svg" target="_blank"><img src="https://raw.githubusercontent.com/NHSDigital/NHSDigital-FHIR-BookingAndReferrals/main/BaRS-images/images/Versioning/API_Interactions-1.1.0.svg" width="1800"/></img></a>


### CapabilityStatement (step 2)

The CapabilityStatement, coupled with the Accept header can define what version of Core the receiver is using. This ties in with the API spec which the CapabilityStatement mimics in terms of functions/features. The capability statement will return a list of message definitions for a given endpoint.

<a href="https://raw.githubusercontent.com/NHSDigital/NHSDigital-FHIR-BookingAndReferrals/main/BaRS-images/images//Versioning/CapabilityStatement-1.1.0.svg" target="_blank">
<img src="https://raw.githubusercontent.com/NHSDigital/NHSDigital-FHIR-BookingAndReferrals/main/BaRS-images/images/Versioning/CapabilityStatement-1.1.0.svg" width="1200"/></img></a>

### MessageDefinition (step 3)

The serviceID will help dictate what MessageDefinitions are returned and ensure they are specifiic to the service being queried. The version of the MessageDefinitions returned would be linked to the version of the Use case. The use case is identified using the useContext element.

For example, a service could service multiple applications covered by a single message definition, of varying versions. They would then choose the version of the message definition most appropriate for the use case. Knowing, from Service Discovery, that the Receiver accepts that type of referral and that it requires that version of the messageDefinition.

This is describes version control at the BaRS use case level.

<a href="https://raw.githubusercontent.com/NHSDigital/NHSDigital-FHIR-BookingAndReferrals/main/BaRS-images/images//Versioning/MessageDefinition-1.1.0.svg" target="_blank"><img src="https://raw.githubusercontent.com/NHSDigital/NHSDigital-FHIR-BookingAndReferrals/main/BaRS-images/images/Versioning/MessageDefinition-1.1.0.svg" width="1700"/></img></a>


