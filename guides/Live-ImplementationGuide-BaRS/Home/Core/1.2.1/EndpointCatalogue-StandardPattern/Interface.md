---
topic: core-StandardPattern-Endpoint-Interface-1.2.1
---

# Interface

The Interface for managing the 3 resources relating to an "endpoint" is detailed below and is part of the [API Specification](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_2_0) for Core 1.2.0 and above. 

## Request and Response 

<table><thead>
  <tr>
    <th>Behaviour</th>
    <th>Initiator</th>
    <th>VERB</th>
    <th>API Path</th>
    <th>Parameters</th>
    <th>Payload</th>
    <th>Payload Definition</th>
    <th>Reactor</th>
    <th>Reactor Behaviour</th>
    <th>Happy Response</th>
    <th>Response Definition</th>
  </tr></thead>
<tbody>
  <tr>
    <td>Get Capabilities</td>
    <td>Sender</td>
    <td>GET</td>
    <td>/metadata</td>
    <td>N/A</td>
    <td>N/A</td>
    <td>N/A</td>
    <td>Endpoint Catalogue</td>
    <td>Return a capability statement&nbsp;&nbsp;&nbsp;describing capabilities.</td>
    <td>200: CapabilityStatement</td>
    <td><a href="https://www.hl7.org/fhir/capabilitystatement.html">https://www.hl7.org/fhir/capabilitystatement.html</a></td>
  </tr>
  <tr>
    <td rowspan="2">Get&nbsp;&nbsp;&nbsp;Endpoints</td>
    <td rowspan="2">Sender / Receiver /&nbsp;&nbsp;&nbsp;BaRS / Admin</td>
    <td rowspan="2">GET</td>
    <td rowspan="2">/Endpoint</td>
    <td>query: _has</td>
    <td>N/A</td>
    <td>N/A</td>
    <td>Endpoint Catalogue</td>
    <td>Return a searchset of Endpoints&nbsp;&nbsp;&nbsp;based on the properties of the parent given as a _has&nbsp;&nbsp;&nbsp;HealthcareService.Identifier or Id</td>
    <td>200: Search Bundle</td>
    <td><a href="https://simplifier.net/guide/NHSBookingandReferrals/UKCore-Bundle">https://simplifier.net/guide/NHSBookingandReferrals/UKCore-Bundle&nbsp;&nbsp;&nbsp;searchset</a></td>
  </tr>
  <tr>
    <td><a href="https://www.hl7.org/fhir/organization.html">query:&nbsp;&nbsp;&nbsp;Endpoint.identifier</a></td>
    <td>N/A</td>
    <td>N/A</td>
    <td>Endpoint Catalogue</td>
    <td>Return a searchset of Endpoints&nbsp;&nbsp;&nbsp;based on the identifier of the Endpoint itself. this should only be one item.</td>
    <td>200:&nbsp;&nbsp;&nbsp;Search Bundle</td>
    <td><a href="https://simplifier.net/guide/NHSBookingandReferrals/UKCore-Bundle">https://simplifier.net/guide/NHSBookingandReferrals/UKCore-Bundle&nbsp;&nbsp;&nbsp;searchset</a></td>
  </tr>
  <tr>
    <td>Get&nbsp;&nbsp;&nbsp;Endpoint</td>
    <td>Sender / Receiver / BaRS / Admin</td>
    <td>GET</td>
    <td>/Endpoint/{id}</td>
    <td>path: id</td>
    <td>N/A</td>
    <td>N/A</td>
    <td>Endpoint Catalogue</td>
    <td>Return specific Endpoint based&nbsp;&nbsp;&nbsp;on id given.</td>
    <td>200: Endpoint</td>
    <td><a href="https://fhir.hl7.org.uk/StructureDefinition/UKCore-Endpoint">https://fhir.hl7.org.uk/StructureDefinition/UKCore-Endpoint</a></td>
  </tr>
  <tr>
    <td>Create&nbsp;&nbsp;&nbsp;Endpoint</td>
    <td>Receiver / Admin</td>
    <td>POST</td>
    <td>/Endpoint</td>
    <td>path: id</td>
    <td>Endpoint</td>
    <td><a href="https://fhir.hl7.org.uk/StructureDefinition/UKCore-Endpoint">https://fhir.hl7.org.uk/StructureDefinition/UKCore-Endpoint</a></td>
    <td>Endpoint Catalogue</td>
    <td>Store a new Endpoint based on id&nbsp;&nbsp;&nbsp;given.</td>
    <td>201: Endpoint</td>
    <td><a href="https://fhir.hl7.org.uk/StructureDefinition/UKCore-Endpoint">https://fhir.hl7.org.uk/StructureDefinition/UKCore-Endpoint</a></td>
  </tr>
  <tr>
    <td>Update&nbsp;&nbsp;&nbsp;Endpoint</td>
    <td>Receiver / Admin</td>
    <td>PUT</td>
    <td>/Endpoint/{id}</td>
    <td>path: id</td>
    <td>Endpoint</td>
    <td><a href="https://fhir.hl7.org.uk/StructureDefinition/UKCore-Endpoint">https://fhir.hl7.org.uk/StructureDefinition/UKCore-Endpoint</a></td>
    <td>Endpoint Catalogue</td>
    <td>Update an existing endpoint&nbsp;&nbsp;&nbsp;based on id given.</td>
    <td>200: Endpoint</td>
    <td><a href="https://fhir.hl7.org.uk/StructureDefinition/UKCore-Endpoint">https://fhir.hl7.org.uk/StructureDefinition/UKCore-Endpoint</a></td>
  </tr>
  <tr>
    <td>Delete&nbsp;&nbsp;&nbsp;Endpoint</td>
    <td>Receiver / Admin</td>
    <td>DELETE</td>
    <td>/Endpoint/{id}</td>
    <td>path: id</td>
    <td>N/A</td>
    <td>N/A</td>
    <td>Endpoint Catalogue</td>
    <td>Remove an existing endpoint&nbsp;&nbsp;&nbsp;based on id given</td>
    <td>200: OperationOutcome</td>
    <td><a href="https://fhir.hl7.org.uk/StructureDefinition/UKCore-OperationOutcome">https://fhir.hl7.org.uk/StructureDefinition/UKCore-OperationOutcome</a></td>
  </tr>
  <tr>
    <td>Get Organisations</td>
    <td>Sender / Receiver / BaRS / Admin</td>
    <td>GET</td>
    <td>/Organisation?</td>
    <td><a href="https://www.hl7.org/fhir/organization.html">query:&nbsp;&nbsp;&nbsp;Organization.identifier</a></td>
    <td>N/A</td>
    <td>N/A</td>
    <td>Endpoint Catalogue</td>
    <td>Return a list of Organizations&nbsp;&nbsp;&nbsp;based on the identifier given</td>
    <td>200: Search Bundle</td>
    <td><a href="https://simplifier.net/guide/NHSBookingandReferrals/UKCore-Bundle">https://simplifier.net/guide/NHSBookingandReferrals/UKCore-Bundle&nbsp;&nbsp;&nbsp;searchset</a></td>
  </tr>
  <tr>
    <td>Get&nbsp;&nbsp;&nbsp;Organisation</td>
    <td>Sender / Receiver / BaRS / Admin</td>
    <td>GET</td>
    <td>/Organisation/{id}</td>
    <td>path: id</td>
    <td>N/A</td>
    <td>N/A</td>
    <td>Endpoint Catalogue</td>
    <td>Return a specific Endpoint based&nbsp;&nbsp;&nbsp;on the id given.</td>
    <td>200: Organization</td>
    <td><a href="https://fhir.hl7.org.uk/StructureDefinition/UKCore-Organization">https://fhir.hl7.org.uk/StructureDefinition/UKCore-Organization</a></td>
  </tr>
  <tr>
    <td>Create&nbsp;&nbsp;&nbsp;Organisation</td>
    <td>Receiver / Admin</td>
    <td>POST</td>
    <td>/Organisation</td>
    <td>path: id</td>
    <td>Organization</td>
    <td><a href="https://fhir.hl7.org.uk/StructureDefinition/UKCore-Organization">https://fhir.hl7.org.uk/StructureDefinition/UKCore-Organization</a></td>
    <td>Endpoint Catalogue</td>
    <td>Store a new Organization based&nbsp;&nbsp;&nbsp;on the id given.</td>
    <td>201: Organization</td>
    <td><a href="https://fhir.hl7.org.uk/StructureDefinition/UKCore-Organization">https://fhir.hl7.org.uk/StructureDefinition/UKCore-Organization</a></td>
  </tr>
  <tr>
    <td>Update&nbsp;&nbsp;&nbsp;Organisation</td>
    <td>Receiver / Admin</td>
    <td>PUT</td>
    <td>/Organisation/{id}</td>
    <td>path: id</td>
    <td>Organization</td>
    <td><a href="https://fhir.hl7.org.uk/StructureDefinition/UKCore-Organization">https://fhir.hl7.org.uk/StructureDefinition/UKCore-Organization</a></td>
    <td>Endpoint Catalogue</td>
    <td>Update an existing Organization&nbsp;&nbsp;&nbsp;based on the id given.</td>
    <td>200: Organization</td>
    <td><a href="https://fhir.hl7.org.uk/StructureDefinition/UKCore-Organization">https://fhir.hl7.org.uk/StructureDefinition/UKCore-Organization</a></td>
  </tr>
  <tr>
    <td>Delete&nbsp;&nbsp;&nbsp;Organisation</td>
    <td>Receiver / Admin</td>
    <td>DELETE</td>
    <td>/Organisation/{id}</td>
    <td>path: id</td>
    <td>N/A</td>
    <td>N/A</td>
    <td>Endpoint Catalogue</td>
    <td>Remove an existing Organization&nbsp;&nbsp;&nbsp;based on the id given.</td>
    <td>200: OperationOutcome</td>
    <td><a href="https://fhir.hl7.org.uk/StructureDefinition/UKCore-OperationOutcome">https://fhir.hl7.org.uk/StructureDefinition/UKCore-OperationOutcome</a></td>
  </tr>
  <tr>
    <td rowspan="2">Get HealthcareService</td>
    <td rowspan="2">Sender / Receiver /&nbsp;&nbsp;&nbsp;BaRS / Admin</td>
    <td rowspan="2">GET</td>
    <td rowspan="2">/HealthcareService</td>
    <td>query:&nbsp;&nbsp;&nbsp;HealthcareService.identifier</td>
    <td>N/A</td>
    <td>N/A</td>
    <td>Endpoint Catalogue</td>
    <td>Return a list of&nbsp;&nbsp;&nbsp;HealthcareServices based on the identifier given</td>
    <td>200: Search Bundle</td>
    <td><a href="https://simplifier.net/guide/NHSBookingandReferrals/UKCore-Bundle">https://simplifier.net/guide/NHSBookingandReferrals/UKCore-Bundle&nbsp;&nbsp;&nbsp;searchset</a></td>
  </tr>
  <tr>
    <td>query:&nbsp;&nbsp;&nbsp;HealthcareService.providedBy</td>
    <td>N/A</td>
    <td>N/A</td>
    <td>Endpoint Catalogue</td>
    <td>Return a list of&nbsp;&nbsp;&nbsp;HealthcareServices based on the identifier given</td>
    <td>200: Search Bundle</td>
    <td><a href="https://simplifier.net/guide/NHSBookingandReferrals/UKCore-Bundle">https://simplifier.net/guide/NHSBookingandReferrals/UKCore-Bundle&nbsp;&nbsp;&nbsp;searchset</a></td>
  </tr>
  <tr>
    <td>Get&nbsp;&nbsp;&nbsp;HealthcareService</td>
    <td>Sender / Receiver / BaRS / Admin</td>
    <td>GET</td>
    <td>/HealthcareService/{id}</td>
    <td>path: id</td>
    <td>N/A</td>
    <td>N/A</td>
    <td>Endpoint Catalogue</td>
    <td>Return a specific&nbsp;&nbsp;&nbsp;HealthcareServicesbased on the id given.</td>
    <td>200: HealthcareServices</td>
    <td><a href="https://fhir.hl7.org.uk/StructureDefinition/UKCore-Organization">https://fhir.hl7.org.uk/StructureDefinition/UKCore-Organization</a></td>
  </tr>
  <tr>
    <td>Create&nbsp;&nbsp;&nbsp;HealthcareService</td>
    <td>Receiver / Admin</td>
    <td>POST</td>
    <td>/HealthcareService</td>
    <td>path: id</td>
    <td>Organization</td>
    <td><a href="https://fhir.hl7.org.uk/StructureDefinition/UKCore-Organization">https://fhir.hl7.org.uk/StructureDefinition/UKCore-Organization</a></td>
    <td>Endpoint Catalogue</td>
    <td>Store a new&nbsp;&nbsp;&nbsp;HealthcareServicesbased on the id given.</td>
    <td>201: HealthcareServices</td>
    <td><a href="https://fhir.hl7.org.uk/StructureDefinition/UKCore-Organization">https://fhir.hl7.org.uk/StructureDefinition/UKCore-Organization</a></td>
  </tr>
  <tr>
    <td>Update&nbsp;&nbsp;&nbsp;HealthcareService</td>
    <td>Receiver / Admin</td>
    <td>PUT</td>
    <td>/HealthcareService/{id}</td>
    <td>path: id</td>
    <td>Organization</td>
    <td><a href="https://fhir.hl7.org.uk/StructureDefinition/UKCore-Organization">https://fhir.hl7.org.uk/StructureDefinition/UKCore-Organization</a></td>
    <td>Endpoint Catalogue</td>
    <td>Update an existing&nbsp;&nbsp;&nbsp;HealthcareServicesbased on the id given.</td>
    <td>200: HealthcareServices</td>
    <td><a href="https://fhir.hl7.org.uk/StructureDefinition/UKCore-Organization">https://fhir.hl7.org.uk/StructureDefinition/UKCore-Organization</a></td>
  </tr>
  <tr>
    <td>Delete&nbsp;&nbsp;&nbsp;HealthcareService</td>
    <td>Receiver / Admin</td>
    <td>DELETE</td>
    <td>/HealthcareService/{id}</td>
    <td>path: id</td>
    <td>N/A</td>
    <td>N/A</td>
    <td>Endpoint Catalogue</td>
    <td>Remove an existing&nbsp;&nbsp;&nbsp;HealthcareServicesbased on the id given.</td>
    <td>200: OperationOutcome</td>
    <td><a href="https://fhir.hl7.org.uk/StructureDefinition/UKCore-OperationOutcome">https://fhir.hl7.org.uk/StructureDefinition/UKCore-OperationOutcome</a></td>
  </tr>
</tbody></table>

## Parameters

This table describes the parameters currently defined for the Paths defined in the interface table above.

<table><thead>
  <tr>
    <th>API Path</th>
    <th>Type</th>
    <th>Parameter</th>
    <th>Format</th>
    <th>Purpose</th>
  </tr></thead>
<tbody>
  <tr>
    <td rowspan="2">/Endpoint?</td>
    <td rowspan="2">query</td>
    <td rowspan="2">_has</td>
    <td>_has:HealthcareService.Identifier=<a href="https://fhir.nhs.uk/Id/dos-service-id%7C1000099999">https://fhir.nhs.uk/Id/dos-service-id|1000099999</a></td>
    <td rowspan="2">An identifier for the HealthcareService to which Endpoints belong. in this example an id or DoS id.</td>
  </tr>
  <tr>
    <td rowspan="2">_has:HealthcareService.Id=95852b93-d1ab-4c51-8e7d-c24cf9b257a9</td>
  </tr>
  <tr>
    <td>/Endpoint?</td>
    <td>query</td>
    <td><a href="https://www.hl7.org/fhir/organization.html">Endpoint.identifier</a></td>
    <td>The identifier of the type of Endpoint. This would be used to say if you want a BaRS endpoint or otherwise.<br></td>
  </tr>
  <tr>
    <td>/Endpoint/{}</td>
    <td>path</td>
    <td>id</td>
    <td>GUID/UUID - "c1ab3fba-6bae-4ba4-b257-5a87c44d4a91"</td>
    <td>The identifier of the endpoint.</td>
  </tr>
  <tr>
    <td>/HealthcareService/?</td>
    <td>query</td>
    <td>HealthcareService.identifier</td>
    <td><a href="https://fhir.nhs.uk/Id/dos-service-id%7C1000099999">https://fhir.nhs.uk/Id/dos-service-id|1000099999</a></td>
    <td>an identifier of the healthcareService, in this example, a DoS id.</td>
  </tr>
  <tr>
    <td>/HealthcareService/?</td>
    <td>query</td>
    <td>HealthcareService.providedBy</td>
    <td><a href="https://fhir.nhs.uk/Id/ods-organization-code%7CA001">https://fhir.nhs.uk/Id/ods-organization-code|A001</a></td>
    <td>the owning organisations ODS code.</td>
  </tr>
  <tr>
    <td>/HealthcareService/{id}</td>
    <td>path</td>
    <td>id</td>
    <td>GUID/UUID - "c1ab3fba-6bae-4ba4-b257-5a87c44d4a91"</td>
    <td>specific resource id of an HealthcareService.</td>
  </tr>
  <tr>
    <td rowspan="2">/Organisation?</td>
    <td rowspan="2">query</td>
    <td rowspan="2"><a href="https://www.hl7.org/fhir/organization.html">Organization.identifier</a></td>
    <td>"A001"</td>
    <td rowspan="2">An identifier for the organization. in this example an ODS code. </td>
  </tr>
  <tr>
    <td><a href="https://fhir.nhs.uk/id/ods-organization-code">"https://fhir.nhs.uk/id/ods-organization-code</a>|A001"</td>
  </tr>
  <tr>
    <td>/Organisation/{id}</td>
    <td>path</td>
    <td>id</td>
    <td>GUID/UUID - "c1ab3fba-6bae-4ba4-b257-5a87c44d4a91"</td>
    <td>specific resource id of an organization. </td>
  </tr>
</tbody></table>