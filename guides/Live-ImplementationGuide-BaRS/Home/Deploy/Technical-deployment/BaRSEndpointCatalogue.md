---
topic: configure-endpoint-catalogue
---

## {{page-title}}

Every service receiving messages through BaRS will need their ServiceId and endpoint added to the BaRS Endpoint Catalogue.  This enables the BaRS Proxy to direct messages to the service.  

When a Sender wants to send a booking or referral using the BaRS Proxy, they will use a Service Discovery tool and select the Receiver's service in their system.  

The Sender will include the ServiceId for the selected service in the HTTP Headers [NHSD-Target-identifier](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1.3.0#overview--overview) it sends to the BaRS Proxy.  

The BaRS Proxy uses the ServiceId in the HTTP Header to reference the BaRS Endpoint Catalogue, find the specific endpoint for the service and transport the message to the correct destination. 

### How to add a service to the BaRS Endpoint Catalogue:

* Note the ServiceId used in Service Discovery (NHS Directory of Service or other Service Discovery tool)

* Obtain the service's URL endpoint details from the Receiving supplier or provider.  The endpoint will need to be certified and meet the criteria for connection to the BaRS Proxy.  More details are available in [Connecting as a receiver](https://simplifier.net/guide/nhsbookingandreferralstandard/Home\Build\Testing-and-Environments\Connect-as-a-receiver.page.md) 

* Email: <england.bookingandreferralstandard@nhs.net> with the ServiceId and endpoint details.  State the environment to be configured, INT or PROD, and include planned dates for testing.

**Note**: CareConnect configuration must be maintained alongside the BaRS configuration. This is to ensure senders who are not yet BaRS compliant can still work with CareConnect and GP Connect.

<br>
