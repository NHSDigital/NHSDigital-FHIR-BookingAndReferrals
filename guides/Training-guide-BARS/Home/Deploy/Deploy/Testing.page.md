## {{page-title}}

Testing is a continuous process throughout the development phase and continues right through to business go-live (in the Production environment). There are numerous stages, environments and systems involved and, to ensure there is clarity for suppliers and providers, the BaRS team define the testing stages as outlined below:-

| Testing stage         | NHS Environment  | BaRS API (API-M)             | Solution Environment      | DoS (if required)       |
|-----------------------|------------------|------------------------------|---------------------------|-------------------------|
|API Spec 'Try this API'|Sandbox           |sandbox.api.service.nhs.uk    |                           |                         |
|INT development        |INT               |int.api.service.nhs.uk        | Development (supplier)    |UserTest                 |
|INT assurance          |INT               |int.api.service.nhs.uk        | Development (supplier)    |UserTest                 |
|UAT testing            |INT               |int.api.service.nhs.uk        | UAT (provider)            |UserTest                 |
|Technical Go Live      |Prod              |api.service.nhs.uk            | Production (provider)     |Production               |

#### Test Plans
Planning is essential to successful testing where numerous parties are involved. The test needs careful orchestration and for each of the actors involved to know the plan and their roles and resposibilities within it.

**Test Plans** must be adopted for testing on any live-like environment (**INT** and **Production**). However, there are circumstances where ad hoc testing can occur in the Integration (INT) environment, without the need for a full Test Plan (or all actors). For example, when a supplier is initially deploying and configuring their solution (during their later development phases) to test against other suppliers who are already deployed and assured.

The documented steps in the Test Plan must include:-
* prerequiste steps for the test. For example, a particular patient with a certain condition
* test reference and name
* steps to perform test. For example, create local encounter, select a particular service
* expected result 
* ability to record success or failure

Tests in the plan MAY cover both expected workflows and error states. 

Before engaging in a Test Plan, ensure the follow steps are complete - 
* **Configuration** steps above have been completed
* actors required for the test are informed
* date and time for the testing agreed and scheduled
* test steps are documented (as described above)
* specific test data elements are documented. For example, the patient NHS number to use
* expected results of the test are known and can verified