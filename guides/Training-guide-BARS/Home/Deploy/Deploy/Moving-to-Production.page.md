## {{page-title}}

Appropriate planning is required to ensure the successful go live of a solution. There is a staged approach to moving a solution through to Production, which involves testing and decision making by the actors involved, to satisfy the solution is robust enough for patient contacts. Releasing to Production can only happen once {{pagelink:assure, text:assurance}} is complete and Solution Assurance have issued a Technical Conformance Certificate (TCC). Requests to {{pagelink:Home/Build/Testing-and-Environments/Onboarding.page.md, text:onboard}} to Production infrastructure (**Connection Agreement**) will be rejected prior to this. 

Adopting BaRS is likely to require **organisational change**, which at times may be signifcant (at least at service level), and may need resource from many parties to adopt and implement, including management, clinical and technical teams, as well as system users. A project plan, for implementation and go-live will be required to organise resources accordingly. 

In addition to the Configuration steps outlined above, a Clinical Safety Officer (CSO) must be engaged to understand the impact of the BaRS workflow on the service implementing and the organisation at large. It is expected that **DCB 0160**  Clinical Risk Management: its Application in the Deployment and Use of Health IT Systems will be completed as part of the clinical governance process. This will underpin the Service's Standard Operating Procedures (SOPs) and any training materials required for system users. 

A project plan must be drawn up, documenting the steps from the current (as-is) workflow to the new (to-be) one. This will include core phases:- 
* changes to workflow
* deployment of solution
* testing phases 

#### Roles and Responsibilities 
The actors from the numerous parties must know what is expected of them during a planned test. This ensures the test has the best chance of success and time is not wasted through trial-and-error attempts.

There is a requirement to cover these core roles for any level of planned test. There may be others involved or some individuals may perform multiple roles.  

|Organisation|Expertise|Individual Role|
|:---|:---|:---|
|NHS England|BaRS|Delivery Manager|
|NHS England (regional)|DoS|Configuration Lead|
|Supplier (Software solution*)|Sender (software)|Technical Support|
|Service Provider (e.g. 111 Provider)|Sender|Project Lead|
|Service Provider (e.g. 111 Provider)|Sender|Clinical Lead|
|Service Provider (e.g. 111 Provider)|Sender|System User|
|Supplier (Software solution*)|Receiver (software)|Technical Support|
|Service Provider (e.g. ED)|Receiver|Project Lead|
|Service Provider (e.g. ED)|Receiver|Clinical Lead|
|Service Provider (e.g. ED)|Receiver|System User|

#### User Acceptance Tests (UAT)
As part of the move to Production, the solution will be deployed to the  Provider's testing environment. This must be a replica of the current production environment where the additional BaRS functionality can be trialled to ensure it functions as expected and the system users can be trained to use it. Full functional review of the solution, as well as existing functionalty, should be undertaken during this **Provider Testing** phase. 

All workflows documented in the **Test Plan** must be tested (and pass) in UAT before arranging upgrades and configuration to the Production environment. If issues with the solution are found at this stage they can be rectified, without having any impact on Production, through either configuration or a new release of the solution. This is the best time to find issues, if they exist, so sufficient resource should be dedicated to ensure thorough testing. 

#### Technical Go Live
Assuming the **Provider Testing** has been successful, the **Technical Go Live** can be scheduled. The Technical Go Live testing will take place in the Production environment and will cover all expected functional (happy path) workflows.

Once complete, if all the functional tests have passed, a decision (Go/No Go) to progress to the live environment can be made and a date scheduled.

**NOTE** - Care must be taken at this stage to limit impact on the live services. The testing must be carried out in live but the service cannot technically go live (and deal with patients) until all functional tests in the Test Plan have been completed successfully. 

#### Business Go Live
On the agreed date of Business go-live (which may be straight after the Technical go live) the system will be enabled, ready for live patient use. If the Business go-live is not on the same day as the Technical go-live, a final end-to-end test run, to verify functionality, should take place before the service is declared fit for live use. The solution then moves from a 'project' into BAU (Business as Usual), supported by all usual processes e.g. Technical Support.

#### DoS Leads
If the provider operates within Urgent and Emergency Care (UEC), they are likely to have a UEC Directory of Services (DoS) entry. DoS leads must configure Service Providers who wish to use BaRS in the standard way, as the service dictates, but their DoS ID will also need to exist in the BaRS Endpoint Catalogue.

Steps to configure the provider on the BaRS Endpoint Catalogue:- 
* note the Service ID on DoS
* Obtain API endpoint details for the service from the Supplier or Provider 
* Email <bookingandreferralstandard@nhs.net> with both pieces of information from above, stating the environment to be configured (INT or Prod). You should include the proposed dates for testing (if known) to allow the urgency of the request to be set

**NOTE** -  [CareConnect configuration](https://developer.nhs.uk/apis/uec-appointments/dep_dosoverview.html) must be maintained alongside the BaRS configuration. This is so senders who are not yet BaRS compliant can still work with CareConnect and GP Connect. 