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
* **{{pagelink:design-core, text:Core}}**: BaRS Core components - API Spec, Endpoint Catalogue etc.
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

