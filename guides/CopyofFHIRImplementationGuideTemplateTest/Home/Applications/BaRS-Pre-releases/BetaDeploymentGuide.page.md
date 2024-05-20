---
topic: betadeploymentguide
---

# Beta Deployment Guide


> ℹ️ **Important:** This page is intended as guidance for all parties involved in BaRS beta deployments. For guidance on stable (V1.0 and above) deployments see {{pagelink:deploy, text:deploy}}.


BaRS Applications (the application of the standard to one or more use cases) are being developed following the agile methodology specified in the <a href="https://www.gov.uk/service-manual" target="_blank"> Government Digital Services (GDS) Service Manual</a>. The methodology specifies a <a href= "https://www.gov.uk/service-manual/agile-delivery/how-the-beta-phase-works" target="_blank"> beta phase </a> which is intended as an opportunity to test, learn and iterate the standard collaboratively, first with test, and then with real patient data. This is prior to the publication of a stable (V1.0 and above) version of the standard for widespread use.   

Every BaRS Application needs to be proven in use in a beta phase. During this phase, healthcare IT system suppliers, healthcare providers and NHS England (policy and strategy and the BaRS team) need to work together to deliver specific activities and with the agreed roles and responsibilities described in this document.  

## Who this page is for

This guide describes the key tasks, agreed roles and responsibilities and ways of working for all parties involved in deploying BaRS conformant solutions as part of a new BaRS application throughout the beta phases.  This will involve working with teams across the NHS and supplier landscape and following the activities documented below.   

It is applicable to the following:  

- Healthcare providers  
- Healthcare IT system suppliers    
- BaRS team (NHS England)  
- NHS England Policy and Strategy team (the business area relevant to the use case) 

This guidance does not cover any commercial arrangements between supplier and healthcare provider. 


## Team Charter   

The following team charter outlines the guidelines and expectations for how all parties will work together:  

### Transparency 
All parties will seek to communicate with each other in an open and honest manner and make available the information (as appropriate) and resources that are reasonably required to achieve the aims of the group.  

### Supportive 
All parties will be mindful and protective of the professional reputation of the other organisations. They will act accordingly, resolving any disagreements that may emerge as quickly as possible in a professional manner and agreeing any external communication in relation to such disagreements.  

### Mutual Success
Each organisation will strive to support the success of the other parties involved in the BaRS Application development.  
### Commitment 
All parties will commit to completion of the BaRS Application once they have started.  

### Timescales
Each organisation will endeavour to maintain their development cadence. This is to ensure that all parties (Sending providers and suppliers and receiving suppliers and providers) complete the development at the same time.  

## Acceptance Criteria 

The public beta minimum acceptance criteria for each BaRS Application is determined by the Service Risk Level. This has been agreed with NHS England Clinical Safety Group and recorded in the BaRS Clinical Risk Management Plan. A summary is outlined below. You can find the Service Risk Level for each BaRS application in the <a href= "https://www.gov.uk/service-manual/agile-delivery/how-the-beta-phase-works" target="_blank"> Clinical Safety Case (Appendix A - BaRS Applications) </a>.
 

| Acceptance Criteria                                                                 | Service Risk Level Low | Service Risk Level Medium | Service Risk Level High |
|-------------------------------------------------------------------------------------|------------------------|--------------------------|-------------------------|
| Minimum number of referrals (including responses where relevant)                    | 20                     | 50                       | 75                      |
| Minimum verification period (with no safety-related incidents due to the BaRS implementation) | 14 days                | 28 days                  | 48 days                 |

For the BaRS team to confirm that the beta has successfully completed, a provider will have: 

- Successfully executed all their UAT test plans. 
Completed a minimum number of agreed referrals in line with the BaRS clinical risk management plan. *Note, the referrals could be completed by multiple providers. 
- Completed a period of live running (verification period) proportionate to the level of service risk for the use case. This period must be free from safety related incidents
- Reviewed supporting guidance and shared best practice to support the wider business transformation activity. 


## Key Deployment Activities

The following activities will form the BaRS Application beta phase:

### Business Change

As the aim of the BaRS is to enable digitisation of referral workflows, the provider will need to undertake business change activities to achieve the full benefits of adopting a BaRS conformant solution. This may include:

- Updating workflows and standard operating procedures
- Staff training and communications plans
- Updating business continuity plans
- Updating any reporting requirements
- Creation, and updating, of information governance and data protection policies
- Undertaking benefits analysis and realization activities e.g.:
    -  identifying any system configuration requirements or additional developments to maximise local efficiencies 

### Private Beta Testing

The provider works alongside their supplier throughout the beta phases with support from NHS England, including the BaRS team. See roles and responsibilities for each group [link] below.

Private beta (also referred to as User Acceptance Testing (UAT)) is a period where providers undertake end-to-end testing of their BaRS conformant solutions, using agreed test scripts, on a non-production or testing environment configured in the same way as the provider’s planned production (live) environment. All workflows documented in the Test Plan must be tested (and pass) within the UAT environment before any upgrades and configuration to the production environment can take place. Test issues are managed to resolution which may result in an update to the BaRS, the supplier’s BaRS conformant solution and/or the provider’s system configuration, depending on the root cause of the issue.

This is the best time to find issues, if they exist, so sufficient resource should be dedicated to ensure thorough testing. Private beta also includes the decision of when to move into public beta.

### Public Beta

Public beta is a period of running the BaRS conformant solutions (sender and receiver) in the providers’ production environments using live patient information. This period is determined according to agreed acceptance criteria which are bespoke to each application (see Section 1.3). The acceptance criteria is defined by the NHS England Clinical Safety Group and agreed for each use case in the BaRS Clinical Risk Management Plan.

Prior to beginning the public beta period, end-to-end ‘smoke testing’ - testing of mission-critical processes, is undertaken on the providers’ production environments, using test patient data. Care must be taken at this stage to limit impact on the live services. The testing must be carried out in live but the service cannot technically go live (and deal with patients) until all functional tests in the Test Plan have been completed successfully.

Evaluation of the public beta phase, led by the NHS England BaRS Team will inform any amendments to the beta standard. Following the required updates, the standard will be uplifted to a ‘stable’ (1.0) version.

### Public Beta to Provider Adoption of V1.0 (stable) Standard

Once a stable version of a BaRS application is published (version 1.0 and above) and NHS England has agreed for progression to full rollout, system suppliers should agree a schedule for development and subsequent rollout with NHS England and individual providers.This will be in line with national and regional policy and may include compliance dates to align with the Information Standards Notice or appropriate procurement frameworks.

For Providers that have participated in the beta phase, further change and training activities may be required alongside testing prior to implementing the uplifted 1.0 and above version of the standard. This should be agreed with system suppliers. The supplier should uplift and deploy this version within 3 months of publication.

Providers implementing a system conformant with the live version of the BaRS application will also need to agree a deployment plan [link to deployment page in IGe] covering business change, training, and testing with their system suppliers.

### Roles and Responsibilities

Roles and responsibilities for each party are described below. A ‘RASCI’ matrix can be found in Section 5.

Delivery partners and stakeholders must know what is expected of them during the beta Phase. This ensures the best chance of success and that time is not wasted through trial-and-error attempts.

There is a requirement to cover these core roles for any beta Phase. There may be others involved or some individuals may perform multiple roles.

#### The Healthcare IT System Supplier

The suppliers are responsible for:

- The primary relationship with the healthcare provider
- Providing key contacts throughout the beta process
- Supporting business change activities including training, designing new workflow and procedures
- Completing the development against the BaRS
- Further development changes throughout the duration of the beta
- Conducting testing in a non-production environment
- Providing testing and training documentation required to complete beta
- Installing and updating software
- System configuration
- Onsite/remote support throughout testing
- DCB0129 compliance
- Supporting technical triage process for identified issues
- Providing a timely response and resolution to any issues or incidents reported
- Participating in regular conference calls to discuss any matters arising from the testing
- Attending an end of beta retrospective
- Once version 1.0 of the BaRS Application is published the supplier should uplift and deploy this version within 3 months of publication
- Reporting Live incidents to <a href=" https://digital.nhs.uk/services/spine/spine-mini-service-provider-for-personal-demographics-service/service-management-live-service" target="_blank">National Service Desk </a> who will involve the BaRS Programme, if required.

##### Core staff that should be involved:

- Project Lead
- System User

#### The Healthcare Provider

The Providers are responsible for:

- The primary relationship with the supplier
- Providing key contacts throughout the beta process
- Business change activities. This may include designing future state, gap analysis, updating policies and procedures, training, communications, benefits identification and management
- Ensuring that DCB 0160 has been completed as part of the internal clinical governance process
- Clinical Lead and Clinical Safety Officer to sign off at the end of private beta
- Provision of UAT and Production environments, configuration, and training
- Communications to ensure the whole organization is supportive and understands their beta responsibilities
- Providing feedback on documentation
- Producing UAT Test scripts and performing the testing within the agreed timescales
- Documenting and sharing results of beta with the system supplier and BaRS team
- Reporting any issues identified during the testing in a timely fashion with the supporting information e.g. call reports and call recordings where appropriate
- Participating in regular conference calls to discuss matters arising from the testing
- Reviewing and updating their Information Governance transparency information
- Completing beta exit report
- Participating in beta retrospective with supplier and BaRS team
- Reporting Live incidents to suppliers through the usual service management agreement.

##### Core staff that should be involved:

- Project/Digital Lead
- Clinical Lead
- Information Governance Lead
- Operational Lead
- System User

#### The BaRS Team

The BaRS team are responsible for:

- The development of the Booking and Referral interoperability standard
- Solutions assurance including:
  - Approval of evidence provided as part of the BaRS Onboarding process
  - Issuance of Technical Conformance Certificate prior to connection to BaRS Infrastructure
- Providing feedback to stakeholders on the status of the beta projects
- Supporting business change activities
- Clinical witnessing of private beta (UAT)
- Compliance with DCB0129
- Ensuring any feedback is captured and BaRS is updated accordingly
- Signing off on a successful beta
- Establishing and managing an issue tracking/triage and resolution process during the beta period
- Establishing and maintaining a lessons identified log
- Arranging a retrospective session following the beta phase to capture any feedback for future improvements
- Providing the ability to collate of volumetric information for the beta providers, to inform the measurement of acceptance criteria
- Scheduling, chairing, and facilitating calls with providers and suppliers
- Add UAT and Production environment endpoints to the BaRS Endpoint Catalogue.

##### Core staff that should be involved:

- Project Lead
- Clinical Lead
- Technical Lead

#### NHS England Policy/Strategy Team

The NHS England Policy/Strategy team are responsible for:

- Taking the lead for the service design implications including any policy changes of the referral standard
- Developing a wider implementation plan beyond beta
- Responsible for tracking and realizing the benefits of the BaRS in live
- Incorporating learning into the wider business transformation process and documentation
- Answering any operational or policy related queries.

## Communications

During the beta phase queries and issues will be managed and resolved in the following forums:

- Bi-weekly/weekly calls in the run-up period to live running (once supplier development is complete and assurance ongoing)
- Private MS Teams channel for each supplier
- Go/no-go calls
- Daily calls during the initial period of public beta
- Weekly calls during later weeks of public beta
- End of public beta supplier and provider retrospective

## RASCI Matrix  

### Key

| Key | Description |
|-----|-------------|
| R   | Responsible: Responsible for ensuring task reaches completion |
| A   | Accountable: Accountable for successful delivery of the task  |
| S   | Supporting: Provides support to responsible members |
| C   | Consulted: Gives advice to responsible members  |
| I   | Informed: Kept informed about the task progress and decisions |

### Project Tasks

| Project Tasks                                           | Clinical System Supplier | Healthcare Provider | BaRS Team | NHSE Policy & Strategy |
|---------------------------------------------------------|--------------------------|---------------------|-----------|------------------------|
| **Beta Coordination**                                   |                          |                     |           |                        |
| Beta coordination                                       | R                        | R                   | S         | A                      |
| **Software Development**                                |                          |                     |           |                        |
| Continuous development in line with the BaRS            | R                        | C                   | S         | A                      |
| **Solutions Assurance**                                 |                          |                     |           |                        |
| Approval of evidence | R            | I                  | R         | A                      |
| Issuance of Technical Conformance Certificate | C | I | R | A |
| **Governance**                                          |                          |                     |           |                        |
| DCB 0129 compliance                                     | R                        | I                   | R         | A                      |
| Clinical governance including DCB 0160                  | C                        | R                   | I         | A                      |
| Information governance                                  | S                        | R                   | S         | A                      |
| Beta acceptance criteria met                            | C                        | R                   | R         | A                      |
| **Beta Environments**                                   |                          |                     |           |                        |
| Provide private beta (UAT) environment                  | S                        | R                   | S         | A                      |
| Provide public beta environment (Live)                  | S                        | R                   | S         | A                      |
| Install and update software                             | A                        | R                   | S         | I                      |
| Configuration                                           | R                        | C                   | S         | A                      |
| **Beta Testing**                                        |                          |                     |           |                        |
| Private beta test scripts                               | S                        | R                   | S         | A                      |
| Private beta testing                                    | R                        | R                   | S         | A                      |
| Public beta smoke testing                               | R                        | R                   | S         | A                      |
| **Issue Management**                                    |                          |                     |           |                        |
| Issue management                                        | R                        | R                   | R         | I                      |
| Issue resolution                                        | R                        | R                   | R         | I                      |
| **Business Change**                                     |                          |                     |           |                        |
| Business change activities                              | S                        | R                   | S         | A                      |
| **Lessons Learned**                                     |                          |                     |           |                        |
| Lessons learned process                                 | S                        | S                   | R         | A                      |
| **BaRS (Standard) Development**                         |                          |                     |           |                        |
| Continuous development of the Standard                  | S                        | S                   | R         | A                      |
| **Public Beta Service Management**                      |                          |                     |           |                        |
| Incident reporting                                      | I                        | R                   | S         | A                      |
| Incident management                                     | S                        | S                   | S         | A/R                    |
| Incident resolution                                     | R                        | R                   | R         | A                      |
| **NHSE Policy & Strategy**                              |                          |                     |           |                        |
| Service design and related policy changes               | N/A                      | C                   | I         | R/A                    |
| Implementation plan beyond beta                         | C                        | C                   | I         | R/A                    |
| Benefits management beyond beta                         | N/A                      | C                   | I         | R/A                    |
| Policy support for Healthcare Providers                 | N/A                      | C                   | I         | R/A                    |
