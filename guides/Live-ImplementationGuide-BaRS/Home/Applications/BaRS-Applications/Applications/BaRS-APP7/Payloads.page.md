---
topic: APP7-Payloads
---

## {{page-title}}
The specific guidance around the use of key FHIR resources is described below. 

### MessageHeader Resource
{{pagelink:core-SPMessageHeader-1.1.5, text:Standard Patterns for BaRS Operations}} explains in detail how the **MessageHeader** resource **must** be used. 

The MessageHeader resource for the Booking Request should have the following resource elements set as follows:
* **MessageHeader.eventCoding** - **must** be populated with 'booking-request'
* **MessageHeader.reasonCode** - **must** be 'new' or 'update'
* **MessageHeader.focus** - **must** reference the Appointment FHIR resource
* **MessageHeader.definition** - **must** adhere to [Booking Request](https://simplifier.net/NHSBookingandReferrals/MessageDefinition-BARS-MessageDefinition-Booking-Request/~json) Message definition


### Appointment 
The primary resource in a booking is the Appointment resource. When the request 'message bundle' is created by the Sender and processed by the Receiver, this is the starting point from which the booking is understood. It provides either the detail or references to all key FHIR resources. When a Sender builds the booking FHIR 'message bundle' they **must** ensure the *MessageHeader.focus* references the Appointment resource. 

An important function of the Appointment resource is to link the booking and referral when they are related in a workflow. If the referral is successfully made before the booking, the Sender will have the *ServiceRequest.Id* value (from the synchronous HTTP response) and this **must** be included as a relative reference, under *Appointment.basedOn*, in the booking request. 


<hr>

<div markdown="span" class="alert alert-warning" role="alert"><i class="fa fa-warning"></i>
    <b> Important:</b> 
    The sections below show elements in key resources that extend UK Core. Where no table is present, the basic UK Core resource is used unaltered.
</div>
