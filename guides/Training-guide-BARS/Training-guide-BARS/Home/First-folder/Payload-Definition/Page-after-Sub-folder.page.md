# Urgent Referral Payload 

### Applications using this Definition

111 - ED

999 - CAS

<hr>

### What is it for?

The Payloads in this definition are used for workflows that refer patients into or between urgent care services.

<hr>

### What is it made up of?

There are two payloads in this definition.

1. the request stage of the workflow

2. the response stage of the workflow

<hr>

### Payload Definitions

{{render:CapabilityStatementflows.drawio}}

<hr>

#### BARS MessageDefinition ServiceRequest-Request Referral

When making a request to transfer a patient to a service the BARSMessageDefinition-ServiceRequest-Request Referral Message Definition is used to define how the bundle should be built.


<div class="tab">
  <button class="tablinks active" onclick="openTab(event, 'Table')">Table</button>
  <button class="tablinks" onclick="openTab(event, 'XML')">XML</button>
  <button class="tablinks" onclick="openTab(event, 'JSON')">JSON</button>
</div>

<div id="Table" class="tabcontent" style="display:block">
  <h3>Table</h3>
  {{table:https://fhir.nhs.uk/MessageDefinition/bars-message-servicerequest-request-referral}}
</div>

<div id="XML" class="tabcontent">
  <h3>XML</h3>
  {{xml:https://fhir.nhs.uk/MessageDefinition/bars-message-servicerequest-request-referral}}
</div>

<div id="JSON" class="tabcontent">
  <h3>JSON</h3>
 {{json:https://fhir.nhs.uk/MessageDefinition/bars-message-servicerequest-request-referral}}
</div>

<hr>

## Referral Request workflow

When building a bundle from this message definition the following resources are included:

{{render:bars-map-servicerequest-request-referral}}

<hr>

As can be seen from the diagram, the bundle is made up of the following resources:

#### All Profiles - Bundle Message

{{tree:https://fhir.nhs.uk/StructureDefinition/BARSBundleMessage}}

<hr>

#### BARSMessageHeader-ServiceRequest-Request

The MessageHeader resource carries information such as the sender and receiver as is a wrapper for the message. The event.system and event.code will match the MessageDefinition corresponding values. The definition element has a direct link to the MessageDefinition that will be used to check validation of the Bundle contents.


{{tree:https://fhir.nhs.uk/StructureDefinition/BARSMessageHeader-servicerequest-request, hybrid}}

<hr>

#### BARSServiceRequest-ReuestReferral


{{tree:https://fhir.nhs.uk/StructureDefinition/BARSServiceRequest-request-referral, hybrid}}

<hr>

#### UKCore-HealthcareService resource

http://hl7.org/fhir/StructureDefinition/HealthcareService

https://fhir.hl7.org.uk/StructureDefinition/UKCore-HealthcareService

Defines the UK Core constraints and extensions on the HealthcareService resource for the minimal set of data to query and retrieve healthcare service information.

This profile allows exchange of details of a healthcare service available at a location.


<hr>

#### UKCore-Encounter resource

https://fhir.nhs.uk/StructureDefinition/UKCore-Encounter

Defines the UK Core constraints and extensions on the Encounter resource for the minimal set of data to query and retrieve encounter information.

This profile allows exchange of information about an interaction between an individual and healthcare provider(s) for the purpose of providing healthcare service(s) or assessing the health status of an individual.

<hr>

#### UKCore-CarePlan resource

https://fhir.nhs.uk/StructureDefinition/UKCore-CarePlan

Defines the UK Core constraints and extensions on the CarePlan resource for the minimal set of data to query and retrieve a patient’s Care Plan.

<hr>

#### UKCore-Patient resource

https://fhir.nhs.uk/StructureDefinition/UKCore-Patient

Defines the UK Core constraints and extensions on the Patient resource for the minimal set of data to query and retrieve an individual’s demographic information.

This profile allows exchange of demographics and other administrative information about an individual receiving care or other health-related services.

<hr>

#### UKCore-PractitionerRole resource

https://fhir.nhs.uk/StructureDefinition/UKCore-PractitionerRole

Defines the UK Core constraints and extensions on the PractitionerRole resource for the minimal set of data to query and retrieve practitioner role information.

This profile allows exchange of a specific set of roles, specialties and services that a practitioner may perform at an organisation for a period of time.

<hr>

#### UKCore-Practitioner resource

https://fhir.nhs.uk/StructureDefinition/UKCore-Practitioner

Defines the UK Core constraints and extensions on the Practitioner resource for the minimal set of data to query and retrieve practitioner information.

This profile allows exchange of information about all individuals who are engaged in the healthcare process and healthcare-related services as part of their formal responsibilities and this profile is used for attribution of activities and responsibilities to these individuals.

<hr>

#### UKCore-Organization resource

https://fhir.nhs.uk/StructureDefinition/UKCore-Organization

Defines the UK Core constraints and extensions on the Organization resource for the minimal set of data to query and retrieve organisation information.

This profile allows exchange of a formally or informally recognised grouping of people or organisations formed for the purpose of achieving some form of collective action. Includes companies, institutions, corporations, departments, community groups, healthcare practice groups, etc.

<hr>

#### UKCore-MedicationStatement resource

https://fhir.nhs.uk/StructureDefinition/UKCore-MedicationStatement

Defines the UK Core constraints and extensions on the MedicationStatement resource for the minimal set of data to query and retrieve medication statement information.

This profile allows exchange of a record of a medication that is being consumed by a patient. A MedicationStatement may indicate that the individual may be taking the medication now or has taken the medication in the past or will be taking the medication in the future. The source of this information can be the individual, significant other (such as a family member or spouse), or a clinician.

<hr>

#### UKCore-AllergyIntolerance resource

https://fhir.nhs.uk/StructureDefinition/UKCore-AllergyIntolerance

Defines the UK Core constraints and extensions on the AllergyIntolerance resource for the minimal set of data to query and retrieve allergy information.

Profile Purpose
This profile allows a record of a clinical assessment of an allergy or intolerance; a propensity, or a potential risk to an individual, to have an adverse reaction on future exposure to the specified substance, or class of substance.

Where a propensity is identified, to record information or evidence about a reaction event that is characterised by any harmful or undesirable physiological response that is specific to the individual and triggered by exposure of an individual to the identified substance or class of substance.

Substances include but are not limited to a therapeutic substance administered correctly at an appropriate dosage for the individual; food; material derived from plants or animals; or venom from insect stings.

This resource is used to record physical conditions. It MUST not be used to record preferences for or against types of treatment, for example on religious grounds. For such use cases consider the use of the FHIR Consent resource.

<hr>

#### UKCore-Flag resource

http://hl7.org/fhir/StructureDefinition/Flag

https://fhir.hl7.org.uk/StructureDefinition/UKCore-Flag

Defines the UK Core constraints on the Flag resource to provide information on prospective warnings of potential issues when providing care to the patient.

<hr>

#### UKCore-QuestionnaireResponse resource

https://fhir.nhs.uk/StructureDefinition/UKCore-QuestionnaireResponse

Defines the UK Core constraints and extensions on the QuestionnaireResponse resource for the minimal set of data to query and retrieve a complete or partial list of answers to a set of questions completed when responding to a questionnaire.

This profile describes a structured set of questions and their answers. The questions are ordered and grouped into coherent subsets, corresponding to the structure of the grouping of the questionnaire being responded to.

<hr>

#### UKCore-Observation resource

https://fhir.nhs.uk/StructureDefinition/UKCore-Observation

Defines the UK Core constraints and extensions on the observation resource for the minimal set of data to query and retrieve generic observation information.

<hr>

#### UKCore-Consent resource

https://fhir.nhs.uk/StructureDefinition/UKCore-Consent

Defines the UK Core constraints and extensions on the Consent resource for the minimal set of data to query and retrieve consent information.

<hr>