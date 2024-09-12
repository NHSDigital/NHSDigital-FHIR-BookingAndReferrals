## {{page-title}}

This guidance is specific to the 999 AST to CAS Referral Application. It should be applied alongside the core guidance.

#### UKcore-Encounter resource

|     FHIR Element    |     Cardinality    |     Element Guidance                                                                                                                         |     Additional Guidance    |
|---------------------|--------------------|----------------------------------------------------------------------------------------------------------------------------------------------|----------------------------|
| start               | 0..1               | This SHOULD be populated with   the Call Connect time (T0). If this is not available it SHOULD be populated   with the Call Answer Time (T1) |                            |


#### UKCore-CarePlan resource


|     FHIR Element    |     Cardinality    |     Element Guidance                                                                                      |     Additional Guidance |
|---------------------|--------------------|-----------------------------------------------------------------------------------------------------------|-------------------------|
| system              | 0..1               | * Pathways Symptom Group (SG)   code use ‘https://fhir.nhs.uk/Id/pathways-sg-code’ value                  |                         |
| code                | 0..1               | When you are passing an SG code   this MUST be populated with the SG code                                 |                         |
| display             | 0..1               | When you are passing an SG code   this MUST be populated the SG code description                          |                         |
| system              | 0..1               | * Pathways Symptom Discriminator   (SD) code use ‘https://fhir.nhs.uk/Id/pathways-sd-code’ value          |                         |
| code                | 0..1               | When you are passing an SD code   this MUST be populated with the SD code                                 |                         |
| display             | 0..1               | When you are passing an SD code   this MUST be populated the SD code description                          |                         |
| system              | 0..1               | * Pathways Disposition (DX) code   use ‘https://fhir.nhs.uk/Id/pathways-dx-code’ value                    |                         |
| code                | 0..1               | When you are passing an Dx code this MUST be populated with   the Dx code                                 |                         |
| display             | 0..1               | When you are passing an Dx code   this MUST be populated the Dx code description                          |                         |
| system              | 0..1               | * Ambulance Response Programme   (ARP) code use ‘https://fhir.nhs.uk/Id/pathways-arp-code’ value          |                         |
| code                | 0..1               | When you are passing an ARP code   this MUST be populated with the ARP code                               |                         |
| display             | 0..1               | When you are passing an ARP code   this MUST be populated the ARP code description                        |                         |
| system              | 0..1               | * AMPDS Dispatch Code use   ‘https://fhir.nhs.uk/Id/ampds-code’ value                                     |                         |
| code                | 0..1               | When you are passing an AMPDS   dispatch code this MUST be populated with the AMPDS dispatch code         |                         |
| display             | 0..1               |  When you are passing an AMPDS dispatch code   this MUST be populated the AMPDS dispatch code description |                         |


#### UKCore-Organisation resource

|     FHIR Element    |     Cardinality    |     Element Guidance                                                           |     Additional Guidance    |
|---------------------|--------------------|--------------------------------------------------------------------------------|----------------------------|
| value               | 0..1               | Sender ODS code in the event   that they need to receive an ambulance request. |                            |



#### UKCore-QuestionnaireResponse resource

This resource is used to communicate links to external sources of clinical information used in the triage/assessment of the patient that would be useful to the recipient.