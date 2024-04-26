---
topic: core-FHIRUsage-FHIR-Operations-1.0.3
---

## FHIR Operations framework 

Performing the required steps in workflow using simple CRUD operations on single resources can be complex and relies on prior knowledge or dictates explicit rules around workflow in any given system, for example: a patient must exist before a service request can be made. In order to support complex workflows that utilise composites of resources, simple CRUD operations on sinlge resources would breach some core principles of ReST (e.g. inabililty to maintain stateless communication for example). Therefore BaRS utilises the FHIR operations framework which:

- offers a degree of autonomy to the receiver of the communication in how they process for their system
- is designed to support events, triggering activity between systems, supporting the response workflow requirements identified by many of the BaRS use cases, for example:  999 to CAS Validation Request/Response.

<br>
<hr>