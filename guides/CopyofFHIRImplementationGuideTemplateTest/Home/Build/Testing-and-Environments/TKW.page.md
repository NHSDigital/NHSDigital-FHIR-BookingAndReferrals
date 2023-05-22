## {{page-title}}

### What is TKW?

TKW - Toolkit Workbench - is a tool to assist development and assurance of supplier solutions to meet BaRS (Booking and Referral Standard) requirements.

The tool supports testing of key high-level workflows e.g. a booking routine, including some of asynchronous ones, but is also capable of inspecting low level technical requirements. It reports the output in Validation Reports which clearly indicates to the reader where and why a test has failed. In addition, it supports consistent error states which are often difficult to create but required for development and assurance. 

The BaRS TKW tooling is embedded into the INT environment, encompassing all the same end-to-end BaRS infrastructure that is mirrored in Production, rather than being downloaded and used in isolation. This ensures the same steps to deploy solutions to Production are followed during deployment to INT, and allowing testing of requests/responses to occur under Production-like conditions. Similarly, we're able to incorporate other key components, similar to those used in Production workflows, such as the [UserTest Directory of Services (DoS)](https://usertest.directoryofservices.nhs.uk/app/controllers/home/home.php). In the current {{pagelink:Home/Design/BaRS-Applications/Applications, text:BaRS Applications}}, the TKW tool relies on values in the UserTest DoS to elicit particular behavioural responses. The Sender will populate what are termed 'sentinel' values, such as the NHSD-Target-Identifier, with a particular value and TKW will respond with a certain Capability Statement, MessageDefinition etc. (See the 'Scenarios' section for detail).

It is important for Senders to remember TKW is a stateless receiver and is not checking the relationship between requests (except in a handful of stateful scenarios - outlined below). This is important when developing workflows such as linking a booking and referral and transactional Integrity.

### Using TKW Portal

Suppliers must register a Portal account to start working with TKW but Senders and Receivers will use the tool in slightly different ways due to the nature of the requests/responses they require. Senders, needing somewhere to send requests and Receivers needing something to make requests of their solution. 

During the registration process, the 'Target Identifier' and 'ODS Code' values are important to ensure requests are sent and received appropriately. As a Sender (to TKW), the HTTP Header NHSD-End-User-Organisation must include the ODS Code they registered with because TKW will collate requests based on this value. When reports are downloaded and viewed, only requests with that specific ODS Code in the header will be visible. As a Receiver, once logged into the portal and selecting the request(s) TKW is required to make of your endpoint, they will be directed to the Target Identifier registered against and, equally, downloaded reports will only relate to that specific value. 

- Navigate to https://maitportal.testlab.nhs.uk/
- Click Register and complete the form below

{{render:MAIT-Portal.png}}

- Email <bookingandreferralstandard@nhs.net> for a Target Identifier (this represents you on the Endpoint Catalogue)
- MAIT Team will need enable your account, email <bookingandreferralstandard@nhs.net> to advise this has been created
- Verify the account via email 
- Configure Multi-Factor Authentication 
- Access Portal Home screen 

{{render:MAIT-Portal-Home.png}}

#### Sender 

Once registered, requests can be made of TKW in any given workflow e.g. booking, validation etc. and the tool will record and provide downloadable validation reports for each request made. 

The Scenarios (including Stateful Scenarios) outlined below highlight how to elicit particular behaviour required, note the specific sentinel values for NHSD-Target-Identifier and patient NHS Number. As a Sender, the various requests can be made and TKW will repond accoridngly. 

NB: It is important for Senders to remember TKW is a stateless receiver and is not checking the relationship between requests (except in a handful of stateful scenarios - outlined below). This is important when developing workflows such as linking a booking and referral and transactional Integrity.

#### Receiver

A receiver can access the portal (once registered) to send either individual tests or an entire suite of tests to themselves. From the top menu bar, click 'Receive Requests' and the screen below will present -

The receiver selects the request they wish the TKW to make of their endpoint and clicks 'Execute Selected Tests' (bottom of the page). TKW will indicate when the requests have been processed.

{{render:MAIT-Portal-Requests.png}}

Once all requested tests have been completed, the Validation Report can be downloaded - 

- from the top menu, select 'Download Reports'
- then click on the button 'Download Reports' (this packages the report and makes it available to download locally)
- from the top me, select 'Receiver Reports'
- click on the hyperlink of the required report to download locally (.zip format)

### Scenarios

The TKW will respond to the scenarios outlined below. It does not hold the state of any prior request (unless specified in the Stateful scenarios) and the specific 'sentinel' values (in bold) must be used to elicit the required response where stated. 

NB: where 'Any' NHSD-Target-Identifier is specified, only those highlighted in this table will work for TKW. Any of the NHSD-Target-Identifiers configured for TKW. 

| Suite                 | Test          | BaRS Application   | Sentinel Element                      | Sentinel Value   | Comment   |
|-----------------------|---------------|--------------------|---------------------------------------|------------------|-----------|
|Capability|CS for Booking and Referral receiver|111-ED|NHSD Target Identifier (HTTP Header)|2000011147|Returns CS for Booking and Referral receiver service|
||CS for Referral receiver|111-ED, 999-CAS|NHSD Target Identifier (HTTP Header)|2000076289|Returns CS for Referral receiver service|
||CS for Validation sender|999-CAS|NHSD Target Identifier (HTTP Header)|1374839566|Returns CS for Validation sender service (accepting interim and full validation responses)|
||CS for any other receiving service|BaRS Core|NHSD Target Identifier (HTTP Header)|Any (see comment)|Any NHSD Target Identifier other than those a predefined response is set for (see above)|
|MessageDef|MD for Booking and Referral receiver|111-ED|context (parameter)|2000011147|Returns MD for Booking and Referral receiver service|
||MD for Referral receiver|111-ED, 999-CAS|context (parameter)|2000076289 |Returns MD for Referral receiver service|
||MD for Validation receiver|999-CAS|context (parameter)|2000003366|Returns MD for Validation receiver service|
||MD for Validation sender|999-CAS|context (parameter)|1374839566|Returns MD for Validation sender service (accepting interim and full validation responses)|
||MD for any other receiving service|BaRS Core|context (parameter)|Any (see comment)|Any 'context' parameter other than those a predefined response is set for (see above)|
||MD failed request - HTTP 401|BaRS Core|context (parameter)|FAIL0401|
||MD failed request - HTTP 404|BaRS Core|context (parameter)|FAIL0404|
||MD for invalid MessageDefs|BaRS Core|context (parameter)|2000071898|Returns invalid MessageDefintions (includes Invoice resource) for any workflow|
|Booking|Search for free Slots|BaRS Core|Schedule.actor:HealthcareService (parameter)|2000072489||
||Search for free and busy Slots |BaRS Core|Schedule.actor:HealthcareService (parameter)|2000072489|Must include the parameter 'status=free,busy' or 'status=busy,free'|
||Return no Slots|BaRS Core|Schedule.actor:HealthcareService (parameter)|2000073917||
||Return mandatory Slot response|BaRS Core |Schedule.actor:HealthcareService (parameter)|1503499715|This will only include Slot, Schedule and HealthcareService|
||Slot search failed request - HTTP 408|BaRS Core|Schedule.actor:HealthcareService (parameter)|2000081230|HealthcareService = 2000081230|
||New booking for verified patient |BaRS Core|Patient.identifier (NHS No)|9054613556|The returned Appointment Id = ce1c4ced-2a84-4198-9982-9caf894d0bb7 in HTTP synchronous response|
||Get Booking|BaRS Core|n/a||The returned Appointment Id = ce1c4ced-2a84-4198-9982-9caf894d0bb7|
||Cancel Booking|BaRS Core|n/a||The returned Appointment Id = ce1c4ced-2a84-4198-9982-9caf894d0bb7 (assumed cancel is for this appointment)|
||New booking for a patient with no NHS No.|BaRS Core|Patient.identifier (NHS No)|blank (no NHS No.)|The returned Appointment Id = ce1c4ced-2a84-4198-9982-9caf894d0bb7|
||New booking failed request - HTTP 404|BaRS Core|Patient.identifier (NHS No)|9976150288||
||New booking failed request - HTTP 409|BaRS Core|Patient.identifier (NHS No)|9933902830||
||New booking failed request - HTTP 422|BaRS Core|Patient.identifier (NHS No)|9818556143||
||Get booking failed request - HTTP 501|BaRS Core|n/a||GET must be for Appointment Id 0d440c22-7f25-4c6c-905d-2213d197d02a|
|Referral|New referral for a verified patient|111-ED, 999-CAS|Patient.identifier (NHS No)|9054613556|The returned Service Request Id = 79120f41-a431-4f08-bcc5-1e67006fcae0|
||Get Referral|111-ED, 999-CAS|n/a||The returned Service Request Id = 79120f41-a431-4f08-bcc5-1e67006fcae0|
||Cancel Referral|111-ED, 999-CAS|n/a||The returned Service Request Id = 79120f41-a431-4f08-bcc5-1e67006fcae0 (assumed revoke is for this Service Request)|
||New referral for a patient with no NHS No.|111-ED, 999-CAS|n/a||The returned Service Request Id = 79120f41-a431-4f08-bcc5-1e67006fcae0|
||New referral failed request - HTTP 400|111-ED, 999-CAS|Patient.identifier (NHS No)|9618388816|Request must be for a patient with NHS No - 9618388816 and returns 400|
||New referral failed request - HTTP 500|111-ED, 999-CAS|Patient.identifier (NHS No)|9853944189|Request must be for a patient with NHS No - 9853944189 and returns 500|
||Get Referral - HTTP 405|111-ED, 999-CAS|n/a||GET must be for ServiceRequest Id 61215702-0049-4d76-9807-2123f0a6ca15 and returns 405|
||Get Referral - HTTP 429|111-ED, 999-CAS|n/a||GET must be for ServiceRequest Id 9d280ad9-6dda-46d2-a75e-f5b47b2f4e87 and returns 429|
||Get Referral - HTTP 503|111-ED, 999-CAS|n/a||GET must be for ServiceRequest Id 4d65ddaa-4d09-41cd-87c9-aeb9c0c96352 and returns 503|
|Validation |New validation request |999-CAS|n/a||The validation request will return Service Request id = 0b42eac3-0175-43c8-bbab-efaa8ca31ccf|
||New validation request |999-CAS|Patient.identifier (NHS No)|9945210394|The validation request will return Service Request id = 9e595424-9d67-45db-9a90-03259653cd37 which can be used in subsequent error scenarios 'Get Validation - HTTP 408' (4.6)|
||New validation request|999-CAS|Patient.identifier (NHS No)|9010223337|The validation request will return Service Request id =  c337e8d8-fd5b-4a13-a8e4-0f6f4ac1bb1a which can be used in subsequent error scenarios 'Get Validation - HTTP 501' (4.8)|
||Get validation request |999-CAS|n/a||GET must be for Service Request id = 0b42eac3-0175-43c8-bbab-efaa8ca31ccf|
||Update validation request |999-CAS|n/a||The validation request returned will be Service Request id = 0b42eac3-0175-43c8-bbab-efaa8ca31ccf|
||Cancel validation request|999-CAS|n/a|||
||New validation failed request - HTTP 404|999-CAS|Patient.identifier (NHS No)|9976150288|Request must be for a patient with NHS No - 9976150288 and returns 404|
||New validation failed request - HTTP 409|999-CAS|Patient.identifier (NHS No)|9933902830|Request must be for a patient with NHS No - 9933902830 and returns 409|
||New validation failed request - HTTP 422|999-CAS|Patient.identifier (NHS No)|9818556143|Request must be for a patient with NHS No - 9818556143 and returns 422|
||New validation failed request - HTTP 401|999-CAS|Patient.identifier (NHS No)|9383924314|Request must be for a patient with NHS No - 9383924314 and returns 401|
||Get Validation - HTTP 408|999-CAS|n/a||GET must be for Service Request id = 0b42eac3-0175-43c8-bbab-efaa8ca31ccf and returns 408|
||Get Validation - HTTP 501|999-CAS|n/a||GET must be for Service Request id = c337e8d8-fd5b-4a13-a8e4-0f6f4ac1bb1a and returns 501|
|Response|Full Validation Response|999-CAS|Patient.identifier (NHS No)|9091510129|Trigger a Validation response for full validation|
||Interim validation response |999-CAS|Patient.identifier (NHS No)|9706161317|Trigger a Validation response for interim validation|
||Safeguarding DNA Response|111-ED|Patient.identifier (NHS No)|9054613556|Accept a Response flow for failed Safeguarding|
||Safeguarding DNA Response - HTTP 401|111-ED|Patient.identifier (NHS No)|9383924314|Accept a Response flow for failed Safeguarding and returns a 401|

**UserTest DoS Services**

The sentinel values linked to [UserTest DoS](https://usertest.directoryofservices.nhs.uk/app/controllers/home/home.php) services can be found by searching with the following criteria.

| ServiceId      | Service Name           | PostCode   | Pathway                       | Comment   |
|----------------|------------------------|------------|-------------------------------|-----------|
|2000072489|**TESTING ONLY** BaRS Test Service (TKW)|LS1 4AP|NoseBleed without Injury|A catch-all service supporting multiple workflows. Pathways answers to obtain outcome (No, Yes, No, Yes)|
|2000073917|**TESTING ONLY** BaRS Test Service (TKW 2)|LS1 4AP|NoseBleed without Injury|Pathways answers to obtain outcome (No, Yes, No, Yes)|
|1503499715|**TESTING ONLY** BaRS Test Service (TKW 3)|LS1 4AP|NoseBleed without Injury|Pathways answers to obtain outcome (No, Yes, No, Yes)|
|2000081230|**TESTING ONLY** BaRS Test Service (TKW 4)|LS1 4AP|NoseBleed without Injury|Pathways answers to obtain outcome (No, Yes, No, Yes)|
|2000093816|**TESTING ONLY** BaRS Test Service (TKW 5)|LS1 4AP|NoseBleed without Injury|Digital Referral Roles Only. Pathways answers to obtain outcome (No, Yes, No, Yes)|
|1374839566|**TESTING ONLY** BaRS Test Service (TKW 6)|LS1 4AP|NoseBleed without Injury|Pathways answers to obtain outcome (No, Yes, No, Yes)|
|2000011147|**TESTING ONLY** BaRS Test Service (TKW 7)|LS1 4AP|NoseBleed without Injury|Pathways answers to obtain outcome (No, Yes, No, Yes)|
|2000076289|**TESTING ONLY** BaRS Test Service (TKW 8)|LS1 4AP|NoseBleed without Injury|Pathways answers to obtain outcome (No, Yes, No, Yes)|
|2000003366|**TESTING ONLY** BaRS Test Service (TKW 9)|LS1 4AP|NoseBleed without Injury|Pathways answers to obtain outcome (No, Yes, No, Yes)|
|2000071898|**TESTING ONLY** BaRS Test Service (TKW 10)|LS1 4AP|NoseBleed without Injury|Pathways answers to obtain outcome (No, Yes, No, Yes)|

### Stateful Scenarios 
TKW supports a limited stateful response for 111 to ED requests. This is a simulation of the real-world receiving end-point and mimics the expected behaviour of a Reciever solution.

This stateful behaviour is only demonstrated for a specific patient (**NHS Number 9707606312**) and per NHSD-End-User-Organisation - i.e. state will be persisted only between requests made by the same End User Organisation.

**Note** The stateful server will reset each night which will return all users back to the initial state.

State Transition Table indicating the responses the stateful TKW scenarios will support and the expected responses- 

|Event|Initial State|Appointment Booked State|Referral Created State|
|-----|-------------|------------------------|----------------------|
|Make a Booking|Http 200|Http 409 (Booking already exists)|Http 409 (Booking already exists)|
|Cancel a Booking|Http 400 (The booking this request relates to does not exist)|Http 200|Http 200|
|Create Linked Referral Request|Http 400 (The booking this request relates to does not exist)|Http 200|Http 409 (Referral  already exists)|
|Create Mis-linked Referral Request|Http 400 (The booking this request relates to does not exist)|Http 409 (Referral  is not linked to the correct booking)|Http 409 (Referral  already exists)|
|Cancel Referral Request|Http 400 (The booking this request relates to does not exist)|Http 400 (No Referral - The referral this request relates to does not exist)|Http 200|









