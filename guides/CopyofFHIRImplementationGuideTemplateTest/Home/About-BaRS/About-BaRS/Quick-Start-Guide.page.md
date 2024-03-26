# {{page-title}}

Follow this **Quick Start Guide** to best understand how to approach BaRS:

#### Discover 
We recommend reading the following documentation as part of the discovery stage to inform planning: 
* {{pagelink:about_bars, text:components of BaRS}}  
* {{pagelink:Home/About-BaRS/About-BaRS/Definitions-of-Key-Terms.page.md, text:definition of key terms}}  
* {{pagelink:design-core, text:BaRS Core}} 
* {{pagelink:applications, text:BaRS Applications}}
* [BaRS FHIR API specification](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_0_0)

#### Onboarding
{{pagelink:Home/Build/Testing-and-Environments/Onboarding.page.md, text:Onboarding}} with our platform is a self-service process. This step is required to make requests of the BaRS API and have requests forwarded to your endpoint, as a Receiver. This **must** occur on both Integration (INT) and Production environments. The full {{pagelink:Home/Build/Testing-and-Environments/Onboarding.page.md, text: step-by-guide}} can be followed by any solution on either environment. 

Full details of the security model adopted by the platform can be found under the [security](https://digital.nhs.uk/developer/guides-and-documentation/security-and-authorisation/application-restricted-restful-apis-signed-jwt-authentication) section.

#### Design
The following sections provide the essential information needed to design and build a BaRS compliant solution. BaRS is devised in a way to support re-use of functionality across multiple uses cases, to this end the implementation guidance is split into {{pagelink:design-core, text:BaRS Core}} and {{pagelink:applications, text:BaRS Application}} sections. All solutions **must** build the Core and add the specific requirements of the Application to support the given use case. BaRS Core is not sufficient on its own, an Application will always be required. 

#### End-to-end workflow 
When developing against the standard, understanding the {{pagelink:core-EndToEndWorkflow-1.1.3, text:end-to-end workflow}} is key. This section of the guide describes how a solution interacts with the BaRS API, along with the assumptions and expectations of Senders and Receivers. These are the roles suppliers will adopt when building a solution. This guide is written predominantly from the perspective of the request; the Sender and Receiver of the request. However, if the BaRS Application include a response workflow these roles swap, the Sender becoming the Receiver and vice versa. 

BaRS includes several {{pagelink:applications, text:BaRS Application (use cases)}}, each of which supports multiple use cases that share a common workflow and data model.


#### API Spec
The BaRS [API specification](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_0_0) provides detail of the structure of endpoints. The specification allows you to 'Try this API', calling endpoints to view anticipated responses. This is a purely technical document and must be read in conjunction with implementation guidance to build a compliant solution. 

#### Security
All {{pagelink:core-Security-1.1.3, text:security}} is provided through our platform. There are two methods for securing interactions via BaRS API:
* senders will [generate an access token](https://digital.nhs.uk/developer/guides-and-documentation/security-and-authorisation/application-restricted-restful-apis-signed-jwt-authentication#how-this-pattern-works) from the platform and use this to authenticate with the BaRS API. Additionally, requests will include HTTP header values identifying the organisation, software and user, which are passed through the BarS API to Receivers who apply their own access control to the request based on the headers content.
* for Receivers accepting requests, the BaRS API secures the connection with the Receiver using TLS MA, using an [NHS Root CA issued certificate](https://digital.nhs.uk/services/path-to-live-environments/live-environment#rootca-and-subca-certificates). The HTTP header values (as described above) are also passed through. This provides the Receiver with sufficient information to accept or reject the request without having to inspect the payload body. 

##### Error Handling 
{{core-failure_scenarios-1.1.3, text:Error handling}} is an important part of the standard for two key reasons:

* to ensure workflow is as smooth and seamless as possible, the error responses returned **must** be clear to allow the appropriate next action to take place, for example, to include a missing element of information (highlighted by the error response).
* there are several levels of interactions occurring from the Sender, through BaRS API to the Receiver and clearly identifying where the fault lies is important for swift resolution. All implementations **must** adhere to the {{core-failure_scenarios-1.1.3, text:error handling guidance}} which is part of the {{pagelink:assure, text:assurance}} process.

#### Build
##### Environments
The principle environment for development and testing is the INT (integration) environment. This is a like-live environment, harnessing full security and functionality that can expect to be encountered in Production. In addition, the BaRS API specification links to the Sandbox environment, which is capable of demonstrating the key functionality but without the security overhead. 



##### Toolkit Workbench (TKW)
{{pagelink:build-testing, text:TKW - Toolkit Workbench}} - is a tool to assist development and assurance of supplier solutions to become BaRS compliant.

The tool supports testing of key high-level workflows e.g. a booking routine, including the asynchronous flows, as well as being capable of inspecting low level technical requirements. It reports the output in Validation Reports which clearly indicate to the reader where and why a test has failed. In addition, the tool supports consistent error states which are often difficult to create but required for development and assurance. TKW is deployed to the INT enviornment and, therefore, requests/responses will occur under Production like conditions.

#### Assure
{{pagelink:assure, text:Assurance}} for BaRS is achieved by completing and providing evidence, via a Supplier Conformance Assessment List (SCAL), through the Digital Onboarding Portal.

**Supplier Conformance Assessment List (SCAL)**
</p>
To complete assurance you need to:

* complete all SCAL sections through the Digital Onboarding Portal
* provide evidence and supporting diagrams which will enable the Solution Assurance Team to understand the solution and ensure it meets the required standard
* demonstrate an end-to-end test of solution functionality within the integration environment (INT)
* Provide evidence of compliance with DCB0129: Clinical Risk Management: its Application in the Manufacture of Health IT Systems
* State that you have reviewed the BaRS Clinical Safety Case Report and Hazard Log, have integrated transferred risks into your own Hazard Log and have implemented appropriate mitigation as stipulated

#### Deploy
Once a solution is developed (and assured, if deploying to Production) it can be deployed. This stage involves installing, configuring and thoroughly testing the solution to ensure it behaves as intended and users are conversant with all aspects of functionality. It is likely to involve numerous parties across multiple organisations and require meticulous planning. The guidance provided is a suggested check-list of steps to consider and is not exhaustive. 