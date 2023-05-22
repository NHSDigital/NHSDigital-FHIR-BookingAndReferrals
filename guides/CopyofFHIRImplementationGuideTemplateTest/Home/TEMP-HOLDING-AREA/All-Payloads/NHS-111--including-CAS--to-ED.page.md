## {{page-title}}

This guidance is specific to the NHS 111 (including CAS) to ED application. It should be applied alongside the core guidance.

#### BARS ServiceRequest-Request Referral

|     FHIR Element    |     Cardinality    |     Element Guidance                                                                                                |     Additional Guidance    |
|---------------------|--------------------|---------------------------------------------------------------------------------------------------------------------|----------------------------|
| supportingInfo      | 0..1               | This is used to indicate   RejectedServices (Flag and Questionnaire Repsonse) or link to an Appointment   resource  |                            |
| reference           | 0..1               | reference to Rejected Service   Questionnaire or Flag or, alternatively, link to an Appointment                     |                            |
| display             | 0..1               | Display info                                                                                                        |                            |


#### UKCore-Encounter resource

|     FHIR Element    |     Cardinality    |     Element Guidance                                                                                                                                                       |     Additional Guidance |
|---------------------|--------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------|
| start               | 0..1               | This SHOULD be populated with   the time the contact with the practicioner was established. This SHOULD be   the  contact immediately prior to the   referral being sent.  |                         |

#### UKCore-CarePlan resource

|     FHIR Element    |     Cardinality    |     Element Guidance                                                                             |     Additional Guidance    |
|---------------------|--------------------|--------------------------------------------------------------------------------------------------|----------------------------|
| system              | 0..1               | * Pathways Symptom Group (SG)   code use ‘https://fhir.nhs.uk/Id/pathways-sg-code’ value         |                            |
| code                | 0..1               | When you are passing an SG code   this MUST be populated with the SG code.                       |                            |
| display             | 0..1               | When you are passing an SG code   this MUST be populated the SG code description                 |                            |
| system              | 0..1               | * Pathways Symptom Discriminator   (SD) code use ‘https://fhir.nhs.uk/Id/pathways-sd-code’ value |                            |
| code                | 0..1               | When you are passing an SD code   this MUST be populated with the SD code                        |                            |
| display             | 0..1               | When you are passing an SD code   this MUST be populated the SD code description                 |                            |
| system              | 0..1               | * Pathways Disposition (DX) code   use ‘https://fhir.nhs.uk/Id/pathways-dx-code’ value           |                            |
| code                | 0..1               | When you are passing an Dx code   this MUST be populated with the Dx code                        |                            |
| display             | 0..1               | When you are passing an Dx code   this MUST be populated the Dx code description                 |                            |


#### UKCore-Organisation resource

|     FHIR Element    |     Cardinality    |     Element Guidance          |     Additional Guidance |
|---------------------|--------------------|-------------------------------|-------------------------|
| value               | 0..1               | Sender ODS code for reference |                         |


#### UKCore-QuestionnaireResponse resource

This resource is used to communicate links to external sources of clinical information used in the triage/assessment of the patient that would be useful to the recipient. It is   also used to communicate details of services rejected by the patient.