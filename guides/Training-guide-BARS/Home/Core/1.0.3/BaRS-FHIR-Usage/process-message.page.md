---
topic: core-FHIRUsage-Process-Message-1.0.3
---

## $process-message 

This specific FHIR operation enables the exchange of complex composites whilst maintaining the principles of REST. The $process-message endpoint will be called at various stages in any of the workflows outlined to fulfil requests such as:

- 'create a booking'
- 'process a referral for validation' 
- 'validation outcome response'

The endpoint receives only POST requests of bundle type 'message', with the required MessageHeader resource dictating how to process and what is deemed the 'focus' (key Resource) of the request. The sender packages up this content, POSTs to the receiver and lets them decide how to consume and process the bundle. 

You must implement a $process-message endpoint to be compliant with BaRS because it is used for initial requests (booking, service request etc.) but also for responses (validation outcome response etc.).

Please see the {{pagelink:Core-StandardPattern-1.0.3, text: Standard Patterns}} for generic guidance for processing messages.

<br>
<hr> 