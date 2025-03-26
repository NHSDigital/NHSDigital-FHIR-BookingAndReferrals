## {{page-title}}

When making a request to transfer a patient to a service the BARSMessageDefinition-ServiceRequest-Request Referral Message Definition is used to define how the bundle should be built.

This Message Definition is built with the following specific values:

| FHIR   Element         | Cardinality | Element Guidance                                    | Additional Guidance                              |
|------------------------|-------------|-----------------------------------------------------|--------------------------------------------------|
| url                    | 1..1        | Business   Identifier for a given MessageDefinition |                                                  |
| status                 | 1..1        | active                                              |                                                  |
| date                   | 1..1        | Date last   changed                                 |                                                  |
| useContext             | 1..1        |                                                     | We   are expecting the UseContext to be a DOS ID |
| useContext.code.system | 1..1        | https://fhir.nhs.uk/Id/dos-service-id               |                                                  |
| useContext.code.code   | 1..1        | dos-id                                              |                                                  |
| event.system           | 1..1        | https://fhir.nhs.uk/CodeSystem/message-events-bars  |                                                  |
| event.code             | 1..1        | servicerequest-request                              |                                                  |
| focus                  | 2..*        |                                                     |        Bundle and MessageHeader resources must be included in a message type Bundle                                         |
| focus.code             | 1..1        | Type of   resource                                  |                                                  |
| focus.profile          | 1..1        | Profile that   must be adhered to by focus          |                                                  |
| focus.min              | 1..1        | Minimum number   of focuses of this type            |                                                  |
| focus.max              | 1..1        | Maximum number   of focuses of this type            |   

<!--
{{tree:https://fhir.nhs.uk/MessageDefinition/bars-message-servicerequest-request-referral,snapshot}}
	
@```
from MessageDefinition
where name = 'BARS Message Definition ServiceRequest - Request Referral'
for focus
select {
    Resource: code,
    URL: profile,
    Cardinality: min.toString() & '..' & max.toString()
}
```-->

#### The bundle is made up of the following resources:



<br>


