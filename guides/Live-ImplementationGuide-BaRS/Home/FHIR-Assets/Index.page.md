---
topic: fhir_assets
---

## {{page-title}}

</br>

The complete directory of FHIR assets can be found on <a href="https://simplifier.net/NHSBookingandReferrals/~introduction" target="_blank">the simplifier project page</a>

**Profiles**

Profiles are the base for the standard and come from two sources: 

- **UK Core**
specifies a set of constraints and/or extensions to specific base HL7 FHIR resources to enable consistent information flows within the UK, to improve health and care outcomes for all citizens
 
- **BaRS**
specifies additional constraints and/or extensions to UK core profiles, that are common for all BaRS Applications

**Cardinalities**

All attributes defined in FHIR have a cardinality measure defined.  This is the minimum and maximum number of times the data element can appear in any instance of the resource type. Failure to conform to the cardinality of a FHIR attribute will lead to a FHIR validation failure. Visit [cardinality in FHIR](https://hl7.org/fhir/conformance-rules.html) for more details. 

**Necessity**

Necessity indicates whether an element is required for the business process to be successful. Visit [Requirement Levels](https://datatracker.ietf.org/doc/html/rfc2119) for definitions.

**Implementation guidance**

Implementation guidance describes how FHIR is utilised and regulated by BaRS to support interoperable business processes.  Guidance includes generating bundles, building BaRS Application workflows and for individual FHIR resource elements. 

**Message definitions**

Message definitions are a key aspect of BaRS. They define the content of payloads in each Application. BaRS payloads are built to ensure the message to the receiving service includes everything needed to progress the patient journey. The receiver defining the request they receive is a BaRS design principle. {{pagelink:principles_prerequesites, text:BaRS principles and prerequisites}}

**Application**

BaRS Applications define workflows and payloads. They can support any number of use-cases with the same requirements. Suppliers build and are assured for specific Applications. As BaRS grows Applications are expected to include more use-cases, supporting re-use of both the BaRS Application and supplier development.    

<hr>