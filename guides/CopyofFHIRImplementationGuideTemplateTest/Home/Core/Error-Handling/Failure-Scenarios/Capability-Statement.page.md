## Check Capabilities GET /metadata

Foreseen failure scenarios are limited for this interaction, in the scope of the receiver. The majority of failures for this stage of workflow is mainly going to be at the sender ascertaining the capabilities of the Receiver and whether they can interact. This is considered the purpose of this endpoint and therefore is not considered a failure.

GET /metadata is the only Endpoint which does not need a Target identifier. Not providing a Target Identifier will result in the Capability Statement of the BaRS Proxy itself. Providing one will expose potential failure scenarios defined in {{pagelink:ErrorHandling-MessageRouting}} . There are also no query or path parameters required meaning the potential failure scenarios are fewer however Transaction Integrity headers are still required. 

### interactions

  ![BaRS FHIR API end-to-end process](https://raw.githubusercontent.com/NHSDigital/booking-and-referral-media/master/src/images/FailureScenarios/metadata-FailureScenarios-1.0.0.svg)