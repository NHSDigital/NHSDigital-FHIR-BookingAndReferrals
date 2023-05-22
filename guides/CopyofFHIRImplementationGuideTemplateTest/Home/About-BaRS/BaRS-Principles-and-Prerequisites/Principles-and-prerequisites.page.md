This page describes BaRS principles and prerequisites for suppliers. Elements of these principles may be governed through the {{pagelink:assure, text:assurance}} process as conformant requirements. These will be reviewed and updated as part of a regular review cycle. 



||BaRS Principles
|-
|1| BaRS requires a service to be identified prior to initiating a BaRS interaction, BaRS is agnostic of the method used to identify the service|
|2| The receiving system supplier is responsible for the safe display of information to the end users of their system 
|3| Reusable workflows will be maintained
|4| Non conformant payloads should be rejected in their entirety
|5| Clinical information from external sources should be referenced in preference to duplicating, where clinically appropriate/unnecessarily (e.g. SCR)
|6| Prior to a sender updating previously transmitted resources, the latest version of the primary resources must first be read from the original receiver and reconciled with locally held information
|7| The receiver always specifies the payload, not the sender
|8| When transporting information, clinical intent must be preserved between systems
|9| Minimise technical burden by building reusable technology that is easy to adopt
|10| Maintain core data structure to support multiple applications
|11| Only workflows identified by research are supported by the standard
|12| Suppliers MUST support continuous development of the standard (see release management) 


||BaRS Prerequisites
|-
|1| Services will profile their services on the Service Directory so that each ServiceID is associated with a single workflow. (All products)
|2| Systems MUST have a public facing internet connection
|3| Systems MUST support JSON formats for all API interactions
|4| Systems SHOULD have a FHIR Server or FHIR functionality in place
|5| Systems SHOULD implement RESTful behaviour patterns
|6| System Suppliers MUST complete the {{pagelink:Home/Build/Testing-and-Environments/Onboarding.page.md, text:BaRS onboarding process}}
|7| Systems MUST support Service Discovery