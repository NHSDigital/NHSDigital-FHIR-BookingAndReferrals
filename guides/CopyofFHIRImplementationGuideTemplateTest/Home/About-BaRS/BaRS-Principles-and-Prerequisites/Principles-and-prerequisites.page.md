This page describes BaRS principles and prerequisites for suppliers. Elements of these principles may be governed through the {{pagelink:assure, text:assurance}} process as conformant requirements. These will be reviewed and updated as part of a regular review cycle. 



**BaRS Principles**

1. BaRS requires a service to be identified prior to initiating a BaRS interaction, BaRS is agnostic of the method used to identify the service|
2. The receiving system supplier is responsible for the safe display of information to the end users of their system 
3. Reusable workflows will be maintained
4. Non conformant payloads should be rejected in their entirety
5. Clinical information from external sources should be referenced in preference to duplicating, where clinically appropriate/unnecessarily (e.g. Summary Care Record (SCR)
6. Prior to a sender updating previously transmitted resources, the latest version of the primary resources must first be read from the original receiver and reconciled with locally held information
7. The receiver always specifies the payload, not the sender
8. When transporting information, clinical intent must be preserved between systems
9. Minimise technical burden by building reusable technology that is easy to adopt
10. Maintain core data structure to support multiple Applications
11. Only workflows identified by research are supported by the standard
12. Suppliers MUST support continuous development of the standard (see release management) 

<br>

**BaRS Prerequisites**

1. Services will profile their services on the Service Directory so that each ServiceID is associated with a single workflow. (All products)
2. Systems MUST have a public facing internet connection
3. Systems MUST support JSON formats for all API interactions
4. Systems SHOULD have a FHIR Server or FHIR functionality in place
5. Systems SHOULD implement RESTful behaviour patterns
6. System Suppliers MUST complete the {{pagelink:Home/Build/Testing-and-Environments/Onboarding.page.md, text:BaRS onboarding process}}
7. Systems MUST support Service Discovery

<br>

**Incident management and incident reporting**

1. It is expected that system suppliers that are compliant with the Booking and Referral Service have an incident management and reporting system or process in place.
2. It is expected that BaRS compliant systems have a form of monitoring and alerting system in place.
3. If after initial triage of an incident, an issue with the BaRS proxy or other up or downstream system is suspected it MUST be reported to the <a href="https://digital.nhs.uk/services/data-services-for-commissioners/incident-and-service-request-process#:~:text=Contact%20the%20National%20Service%20Desk,.nationalservicedesk%40nhs.net." target="_blank">NHS England National Service Desk (NSD)</a> as soon as possible.