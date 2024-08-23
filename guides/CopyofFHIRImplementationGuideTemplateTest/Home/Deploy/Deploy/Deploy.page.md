## {{page-title}}

> ℹ️ **Important:** This page is intended as guidance for all parties involved in deployments of BaRS stable releases (V1.0 and above). For guidance for Beta deployments see the {{pagelink:Home/Applications/BaRS-Pre-releases/BetaDeploymentGuide.page.md text: Beta Deployment Guide}}.

This page describes a typical process to deploy BaRS conformant systems with a stable release (v1.0 and above).   It outlines the tasks and responsibilities for healthcare providers, clinical system suppliers and NHS England. Please note: the deployment process will subject to supplier and provider agreed ways of working. 

## Who this page is for
This guide describes the common tasks, roles and responsibilities for all parties involved in deploying BaRS conformant solutions (healthcare IT systems) as part of a BaRS application in a stable release. This will involve working following the activities documented in section 2 .. below:  

It is applicable to the following: 

- Healthcare providers 
- Clinical system suppliers   
- NHS England

This guidance does not cover any commercial arrangements between supplier and healthcare provider.

## Key Deployment Activities

This section outlines the typical activities involved in a BaRS deployment.

The diagram below highlights the common process steps, with further details provided in the subsequent section.

![Deployment](
https://raw.githubusercontent.com/NHSDigital/booking-and-referral-media/master/src/images/General/Deployment-1.0.0.svg
)

### Business Change

To realise the desired benefits of BaRS, the organisation must undertake business change activities. Note: providers will require view access of the developed user interface and any new functionality to design the future state processes.

This will typically involve:

- mapping current (as-is) operational processes 
- mapping future state (to-be) operational processes in accordance with the new system capabilities and aligned to benefits 
- carrying out gap analysis and developing a change project plan 
- developing new standard operating procedures (SOPs)
- staff communication and engagement 
- staff training (to take place after system deployment and UAT)
- benefits management and realisation 

### Solution Deployment and Configuration

In almost all {{pagelink:applications, text:BaRS Applications}}, a solution will act as a Sender and Receiver and need to perform all {{pagelink:Home/Build/Testing-and-Environments/Onboarding.page.md, text:onboarding}} steps. 

Onboarding must occur for each environment independently; the process is similar for each but the steps must be replicated. 

The core steps to complete technical setup in an environment are:-
* complete {{pagelink:Home/Build/Testing-and-Environments/Onboarding.page.md, text:onboarding}} for the desired environment
* install supplier solution in the given Solution Environment (See Testing section)
* perform any configuration steps to enable BaRS (and related workflows) in the solution 
* provide service identifier* to be configured in the Endpoint Catalogue (BaRS related component)

*This may be a local value or relate to a [directory of service](https://digital.nhs.uk/services/directory-of-services-dos)

**NOTE** - The detail of installing and configuring a solution will differ considerably depending on the supplier and provider(s) involved.

### Testing

Testing is an integral part of the BaRS development and implementation process. The testing process involves multiple stages, {{pagelink:Home\Build\Testing-and-Environments\Environments.page.md, text:environments}} and systems to ensure thorough validation and functionality.


#### Test Plans

Effective planning is crucial for successful testing, especially when multiple parties are involved. Each participant must clearly understand the plan, their specific roles, and their responsibilities.

Test Plans must be implemented for any testing conducted in live-like environments, such as INT and Production. However, in the Integration (INT) environment, ad hoc testing may occur without a full Test Plan or the involvement of all parties. This can happen, for instance, when a supplier is deploying and configuring their solution during the later stages of development to test compatibility with other pre-deployed and assured suppliers.

The Test Plan should include the following documented steps:

- Prerequisite steps: For example, identifying a patient with a specific condition.
- Test reference and name: Clear identifiers for each test.
- Test steps: Detailed instructions, such as creating a local encounter and selecting a particular service.
- Expected results: What the outcome should be.
- Success or failure recording: A method to document whether the test passed or failed.

Test Plans may encompass both expected workflows and error scenarios.

#### User Acceptance Testing (UAT)

In UAT, BaRS functionality can be trialled to ensure it functions as expected.

All workflows documented in the Test Plan must be tested (and pass) in UAT before arranging upgrades and configuration to the Production environment. If issues with the solution are found at this stage they can be rectified, without having any impact on Production, through either configuration or a new release of the solution. This is the best time to find issues, if they exist, so sufficient resource should be dedicated to ensure thorough testing.

#### Technical Go Live

After successful completion of UAT, the Technical Go Live can be scheduled. This phase involves testing in the Production environment, focusing on all expected functional (happy path) workflows. 

Upon completion, if all functional tests are successful, a Go/No Go decision can be made to proceed to the live environment, and a go-live date can be set.

Important: Careful planning is essential to minimize any impact on live services. Testing must occur in the live environment, but the service cannot officially go live (i.e., handle patient interactions) until all functional tests outlined in the Test Plan are successfully 
completed.

### Business Go Live

On the agreed date for Business Go-Live, which may immediately follow Technical Go-Live, the system will be activated for live patient use. If Business Go-Live does not occur on the same day as Technical Go-Live, a final end-to-end test should be conducted to verify functionality before declaring the service fit for live operation.

Afterward, the solution transitions from a 'project' phase to Business as Usual (BAU), where it is supported by standard processes such as Technical Support.

Once in Production and running as business-as-usual (BAU), should an issue with the solution arise, service providers will be expected to follow their existing support processes with their supplier. After investigation, if the issue is thought to lie with the BaRS API or a third party supplier an incident can be raised with the National Service Desk - ssd.nationalservicedesk@nhs.net - who will involve the BaRS Programme, if required.

## Roles and Responsibilities 

Roles and responsibilities for each involved party are described below. A ‘RASCI’ matrix can be found at the end of this page.

#### The Healthcare IT System Supplier

The suppliers are responsible for:

- The primary relationship with the healthcare provider
- Supporting business change activities including training, designing new workflow and procedures
- Completing the development against the BaRS
- Conducting testing in a non-production environment
- Providing testing and training documentation required
- Installing and updating software
- System configuration
- Onsite/remote support throughout testing
- DCB0129 compliance
- Supporting technical triage process for identified issues
- Providing a timely response and resolution to any issues or incidents reported
- Participating in regular conference calls to discuss any matters arising from the testing
- Reporting Live incidents to <a href=" https://digital.nhs.uk/services/spine/spine-mini-service-provider-for-personal-demographics-service/service-management-live-service" target="_blank">National Service Desk </a> who will involve the BaRS Programme, if required.

##### Core staff that should be involved:

- Project Lead
- System User

#### The Healthcare Provider

The Providers are responsible for:

- The primary relationship with the supplier
- Business change activities. This may include designing future state, gap analysis, updating policies and procedures, training, communications, benefits identification and management
- Ensuring that DCB 0160 has been completed as part of the internal clinical governance process
- Clinical Lead and Clinical Safety Officer sign off
- Provision of UAT and Production environments, configuration, and training
- Communications to ensure the whole organization is supportive and understands their responsibilities
- Providing feedback on documentation
- Producing UAT Test scripts and performing the testing within the agreed timescales 
- Reporting any issues identified during the testing in a timely fashion with the supporting information e.g. call reports and call recordings where appropriate
- Participating in regular conference calls to discuss matters arising from the testing
- Reviewing and updating their Information Governance transparency information
- Reporting Live incidents to suppliers through the usual service management agreement.

##### Core staff that should be involved:

- Project/Digital Lead
- Clinical Lead
- Information Governance Lead
- Operational Lead
- System User
