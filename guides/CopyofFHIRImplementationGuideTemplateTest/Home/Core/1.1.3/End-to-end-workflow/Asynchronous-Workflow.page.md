---
topic: core-EndToEndWorkflow-AsyncWorkflow-1.1.3
---


## {{page-title}}

The FHIR $process-message function supports 'async' parameter but BaRS does not employ this, all $process-message requests are synchronous.

However, BaRS does support request-response loops which are asynchronous. An example of this is the Safeguarding DNA response workflow; the sender (NHS 111 Telephony service) sends a referral with a safeguarding concern flag to an Emergency Department, the patient subsequently doesn't attend (DNAs). The Emergency Department receiver is now responsible for sending a response back to the original sender (the NHS 111 Telephony service) to inform them of the DNA.