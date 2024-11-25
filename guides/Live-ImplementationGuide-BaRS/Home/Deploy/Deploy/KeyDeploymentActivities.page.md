## {{page-title}}

This section outlines the typical activities involved in a BaRS deployment.
The diagram below highlights the common process steps, with further details provided in the subsequent section.

 ![Deployment](
https://raw.githubusercontent.com/NHSDigital/NHSDigital-FHIR-BookingAndReferrals/main/BaRS-Images/General/Deployment-1.0.0.svg
)
## Business Change
To realise the desired benefits of BaRS, the organisation must undertake business change activities. Providers will require view access of the developed user interface and any new functionality to design the future state processes.

Business change activities will typically involve:

- mapping current (as-is) operational processes
- mapping future state (to-be) operational processes in accordance with the new system capabilities and aligned to benefits
- carrying out gap analysis and developing a change project plan
- developing new standard operating procedures (SOPs)
- staff communication and engagement
- staff training (to take place after system deployment and UAT)
- benefits management and realisation

## Solution Deployment and Configuration
In almost all {{pagelink:applications, text:BaRS Applications}}, a solution will act as a Sender and Receiver and need to perform all {{pagelink:Home/Build/Testing-and-Environments/Onboarding.page.md, text:onboarding}} steps.

Onboarding must occur for each environment independently; the process is similar for each but the steps must be replicated.
The core steps to complete technical setup in an environment are:
- complete {{pagelink:Home/Build/Testing-and-Environments/Onboarding.page.md, text:onboarding}} for the desired environment
- install supplier solution in the given Solution Environment (See Testing section)
- perform any configuration steps to enable BaRS (and related workflows) in the solution
- provide service identifier* to be configured in the Endpoint Catalogue (BaRS related component)

*This may be a local value or relate to a directory of service

**NOTE** - The detail of installing and configuring a solution will differ considerably depending on the supplier and provider(s) involved.

## Testing
Testing is an integral part of the BaRS development and implementation process. The testing process involves multiple stages, {{pagelink:Home/Build/Testing-and-Environments/Environments.page.md, text:environments}} and systems to ensure thorough validation and functionality.

There are numerous stages, environments, and systems involved. NHS England (BaRS) defines the testing stages as outlined below:

| Testing Stage         | NHS Environment  | BaRS API (API-M)             | Solution Environment      | DoS (if required)       |
|-----------------------|------------------|------------------------------|---------------------------|-------------------------|
| API Spec 'Try this API'| Sandbox          | sandbox.api.service.nhs.uk    |                           |                         |
| INT Development        | INT              | int.api.service.nhs.uk        | Development (supplier)    | UserTest                |
| INT Assurance          | INT              | int.api.service.nhs.uk        | Development (supplier)    | UserTest                |
| UAT Testing            | INT              | int.api.service.nhs.uk        | UAT (provider)            | UserTest                |
| Technical Go Live      | Prod             | api.service.nhs.uk            | Production (provider)     | Production              |

### Integration (INT) Environment

The INT environment is a like-live environment which suppliers can connect into while in development. This can be done without full assurance in place. 

The INT environment will be the first place a solution is fully deployed. This environment allows different suppliers to test their solutions together, as they intend to work in the Production environment. INT requires all the same technical elements to be configured as they would be in a Production environment. 

Once configured, the solution is ready to interact with other suppliers or {{pagelink:Home/Build/Testing-and-Environments/TKW.page.md, text:Toolkit Workbench (TKW)}}. The BaRS Team can help facilitate the process of engagement with other suppliers for the purposes of testing. The supplier must also demonstrate the full functionality of their solution in INT as part of {{pagelink:assure, text:assurance}} and evidence compliance with DCB0129 Clinical Risk Management: its Application in the Manufacture of Health IT Systems 


### Test Plans
Effective planning is crucial for successful testing, especially when multiple parties are involved.

Each participant must clearly understand the plan, their specific roles, and their responsibilities.
Test plans must be implemented for any testing conducted in live-like environments, such as INT and Production. However, in the integration (INT) environment, ad hoc testing may occur without a full Test Plan or the involvement of all parties. This can happen, for instance, when a supplier is deploying and configuring their solution during the later stages of development to test compatibility with other pre-deployed and assured suppliers.
The Test Plan should include the following documented steps:
- Prerequisite steps: For example, identifying a patient with a specific condition.
- Test reference and name: Clear identifiers for each test.
- Test steps: Detailed instructions, such as creating a local encounter and selecting a particular service.
- Expected results: What the outcome should be.
- Success or failure recording: A method to document whether the test passed or failed.

Test Plans may encompass both expected workflows and error scenarios.
### User Acceptance Testing (UAT)
In UAT, BaRS functionality can be trialled to ensure it functions as expected.

All workflows documented in the Test Plan must be tested (and pass) in UAT before arranging upgrades and configuration to the Production environment.

 If issues with the solution are found at this stage they can be rectified, without having any impact on Production, through either configuration or a new release of the solution. This is the best time to find issues, if they exist, so sufficient resource should be dedicated to ensure thorough testing.
### Technical Go Live
After successful completion of UAT, the Technical Go Live can be scheduled. This phase involves testing in the Production environment, focusing on all expected functional (happy path) workflows.
Upon completion, if all functional tests are successful, a Go/No Go decision can be made to proceed to the live environment, and a go-live date can be set.
Important: Careful planning is essential to minimize any impact on live services. Testing must occur in the live environment, but the service cannot officially go live (i.e., handle patient interactions) until all functional tests outlined in the Test Plan are successfully completed.
## Business Go Live
On the agreed date for Business Go-Live, which may immediately follow Technical Go-Live, the system will be activated for live patient use.

 If Business Go-Live does not occur on the same day as Technical Go-Live, a final end-to-end test should be conducted to verify functionality before declaring the service fit for live operation.

Afterward, the solution transitions from a 'project' phase to Business as Usual (BAU), where it is supported by standard processes such as Technical Support.

Once in Production and running as business-as-usual (BAU), should an issue with the solution arise, service providers will be expected to follow their existing support processes with their supplier. After investigation, if the issue is thought to lie with the BaRS API or a third party supplier an incident can be raised with the National Service Desk - ssd.nationalservicedesk@nhs.net - who will involve the BaRS Programme, if required.

<br>

