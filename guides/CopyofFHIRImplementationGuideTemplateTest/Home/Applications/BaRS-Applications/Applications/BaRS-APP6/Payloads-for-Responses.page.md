---
topic: APP6-Payloads
---

## {{page-title}}

<br>

## Referral Response Payload (Status update)
This section provides guidance on the use of key resources, for the Receiver to create an Referral Response (Status update) to return to the Sender. See [ServiceRequest - Response](https://simplifier.net/nhsbookingandreferrals/bars-messagedefinition-servicerequest-response-referral-short) message definition for details of resources required for this payload.

*Note that Receivers will also have to build the capability to receive and process the Referral Request and Cancellation payloads*
<br>

### MessageHeader Resource
For detailed information on the use of MessageHeader please refer to the {{pagelink:core-SPMessageHeader, text:Standard Pattern - Message Header}}. 

The MessageHeader resource in the Referral Response should have the following resource elements set as follows:
* **MessageHeader.eventCoding** - **must** be populated with 'servicerequest-response'
* **MessageHeader.reasonCode** - **must** be 'new'
* **MessageHeader.focus** - **must** reference the Responder's current Encounter FHIR resource
* **MessageHeader.definition** - **must** adhere to [Referral Response](https://simplifier.net/NHSBookingandReferrals/BARS-MessageDefinition-ServiceRequest-Response-Referral-Short/~json) Message definition.
* **MessgeHeader.Response** - **must** be the original request BundleID

### ServiceRequest Resource
The *ServiceRequest* reflects that sent by the Requester, and maintains the active state of the referral. The *ServiceRequest.status* at this point would stay as 'active'.

### Encounter Resource
The Responder's current *Encounter* is the focus resource in the Referral Response. This was originally the 'planned' Encounter created by the Receiver in the synchronous response to the Referral Request. 

This *Encounter* is used to represent the interaction between the patient and the Receiver healthcare service provider. 

When sending an Referral Response the Receiver **must**:
* Include the Receiver's current *Encounter* as the focus resource of the Referral Response
* Include the current *Encounter.status* on the Receiver's current *Encounter*. This is to indicate to the Sender the progress of the case. It also indicates where a Call Assit or Mutual Aid request has been rejected.
* *Encounter.reasonCode* to be included on the Receiver's current *Encounter* to indicate that it is a response message.

<br>

<hr>
<div markdown="span" class="alert alert-warning" role="alert"><i class="fa fa-warning"></i>
    <b> Important:</b> 
    The sections below show elements in key resources that extend UK Core. Where no table is present, the basic UK Core resource is used unaltered.
</div>