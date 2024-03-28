---
topic: APP2-ScopeAndRequirements
---

## {{page-title}}

### Scope Overview

This BaRS Application (Application 2) covers only use cases:
* 111 Online to ED
* 111 Online to UTC
* S&R to ED
* S&R to UTC

The payloads and workflow have been designed to support these services. Other {{pagelink:applications, text:BaRS Applications}} offer scope for alternative use cases.

### Functional Scope
**Service Discovery**
* Establishing a service to direct requests to is a mandatory step in the workflow
* There is no restriction on the service discovery tools used. Any are capable of being supported whether national or proprietary
* The service **must** be configured within the BaRS infrastructure before requests can be made 

**Slot Management**
* Booking slots are the responsibility and ownership of Receivers to maintain and offer to Senders
* All slot requests **must** occur in real-time without caching by either Senders or Receivers
* The returned slots **should** contain sufficient information for Senders to know what they are booking i.e. have a clear 'type', indicate the role and/or gender of the individual performing on behalf of the service, within any given slot

**Booking**
* Allowing bookings for a service is a method of managing capacity 
* A booking may indicate the exact time an individual can expect to be seen, as is traditionally understood when an 'appointment' is made. Alternatively, the booking timeframe could indicate a range through which the individual may be seen by the service
* The slot the booking is made against may also indicate the type of booking e.g. face-to-face or over the phone and the role of the person who will engage with the individual on behalf of the service
* A booking **must** always be accompanied by a referral
* Bookings are an administrative aspect of the workflow and **should <ins>not</ins>** contain clinically pertinent information

**Referral**
* A referral is a request for care on behalf of an individual from one service to another 
* The referral can be sent without prior establish the capacity the service offers
* The referral will contain primarily clinical information, indicating the need of the individual and **should** state the anticipated action required by the Receiving service
* A referral can be made independent of booking but, where a booking is made as part of the same workflow, they **must** be linked
* Key information is expected to be included in a referral, if collected:
    * list of any services rejected prior to the Receiving service being selected, including reason for rejection 

**API-M**
* All requests and response associated with BaRS must occur through the BaRS API Proxy

**Constraints**
* Supporting use of NHS Pathways and NHS Pathways Clinical Content Support (PaCCS) Clinical Decision Support Systems only
* All Service IDs in First of Type (FoT) will be those of Urgent and Emergency Care (UEC) Directory of Services (DoS) 
* DoS 'attributes' for controlling Booking into services are to remain honoured (see "how does it work" section below for more information)
* No guidance provided on display of referral information beyond the {{pagelink:principles_prerequesites, text:Principles for rendering BaRS Payload}}. 
* No additional guidance provided on Slot display for Booking 
* Consent within BaRS will be for Direct-Care only 
* Certificates for Receiving messages to use nhs.uk domains only.
* Receiving endpoints are to be internet facing.
* Limited Search Slot parameters for Booking - Schedule.actor:healthcareService, Start (range), (slot) status
* Clincial Constraints exist - See Hazard Log
* No element level updates to requests. A new request must be generated to change information in a booking or referral request


### Requirements

**Service Discovery** 
* The service **must** support a unique identifier which the Sender extracts to engage in booking and referral workflows

**Slot display** 
* The schedule and related slot(s) **must** contain the actual geographic location (e.g address) of the booking, rather than generic details of the location of the overall service provider.
* The slot **must** contain details of the start/end times of the available slots
* The available slot(s) **must** be capable of being retrieved from any booking Receiver, regardless of the relationship that the consuming user’s organisation has with that service provider 
* Where there are no available slots, the booking Receiver **must** send an appropriate response to indicate this <ins>not</ins> merely an empty response
* Where there are no available slots, the booking Sender **must** present an appropriate message to the user to indicate this
* The booking Receiver **must** return available slots without requiring to know the potential patient details
* Where the booking Receiver has a number of schedules available to fulfil a request (say, when 2 or more clinicians are delivering surgeries at the same site) they **must** return all of those slots as part of the initial response
* If provided, in addition to Healthcare Service, Schedule and Slot, the booking Sender **must** display Delivery Channel and Practitioner Role, Name and Gender
* Booking Receivers **must <ins>not</ins>** default the Delivery Channel value
* A booking Sender **must <ins>not</ins>** assume a booking Receiver will return requested \_includes e.g. Location
  * Booking Sender **must** handle a Slot response without non mandatory FHIR resources 
  * Booking Sender **must** handle a Slot response with FHIR resources not requested

**Booking** 
* The booking Receiver **must** accept the booking request regardless of whether the patient is not known to the service provider
* The booking Receiver **must** accept potential patients who do <ins>not</ins> have a national validated identifier e.g. NHS Number.
* Where a national indentifier is included, it **must** be 'traced and verified', otherwise, the referral Sender **must** <ins>not</ins> include the national indentifer in the request
* Where the booking was <ins>not</ins> successful, the Receiver **must** send an appropriate response. See {{pagelink:core-failure_scenarios-1.1.3, text:failure scenarios}} for more detail.
* Where the booking was <ins>not</ins> successful, the Sender **must** present an appropriate message to the end user. See {{pagelink:core-failure_scenarios-1.1.3, text:failure scenarios}} for more detail.
* The booking Sender **must** send accompanying clinical information in a BaRS referral request
  * The booking Sender's request **must** be referenced in the BaRS referral request (where the booking is made first in the workflow)
  * The booking Receiver **must** link the explicitly related booking and referral requests
* Update to amend a booking request is <ins>not</ins> supported. If a booking Sender wishes to change information in a request they **must** follow the re-book workflow


**Booking outside assessment outcome timeframe** 
* The booking Sender **must** allow clinical users to book outside the assessment outcome timeframe
* The booking Sender **must** present a notification to non-clinical users and prompt to seek clinical approval to book outside the assessment outcome timeframe
* The booking Sender **must** store sufficient data to show where a patient has been booked outside their assessment outcome timeframe


**Referral requires booking (booking only services)** 
* The booking Sender **must** stop the users from making a referral if no booking has been made when the “requirebooking” service attribute is present against the DoS service
* The booking Sender **must** present an appropriate warning message to the user, indicating the specific service requirements
* The booking Sender **must** allow the referral to be sent when a booking is made, the service requirements having been met
* The user **must** be allowed to select an alternative service 


**Referral** 
* The referral Receiver **must** accept the referral request regardless of whether the patient is not known to the service provider
* The referral Receiver **must** accept potential patients who do <ins>not</ins> have a national validated identifier e.g. NHS Number.
* Where a national indentifer is included, it **must** be 'traced and verified', otherwise, the referral Sender **must** <ins>not</ins> include in the request
* Any new or existing safeguarding concern, recorded as part of the assessment, **must** be included in the referral Sender's request
* The referral Receiver **must** clearly identify any included safeguarding concern to the end user
* The referral Receiver **must** accurately represent information made by the Sender to the end user
* Where the referral was <ins>not</ins> successful, the Receiver **must** send an appropriate response. See {{pagelink:core-failure_scenarios-1.1.3, text:failure scenarios}} for more detail.
* Where the referral was <ins>not</ins> successful, the Sender **must** present an appropriate message to the end user. See {{pagelink:core-failure_scenarios-1.1.3, text:failure scenarios}} for more detail.
* The referral Sender **must** include reference to any accompanying BaRS booking related to the referral
  * The referral Sender's request **must** be referenced in the BaRS booking request (where the referral is made first in the workflow)
  * The referral Receiver **must** link the explicitly related booking and referral requests
* Update to amend a referral request is <ins>not</ins> supported. If a referral Sender wishes to change information in a request they **must** follow the re-refer workflow

**Contacts** 
* A minimum of one contact (patient or third party) with a contact method (phone, email, etc.) of phone **must** be provided in requests
* All contacts **must** have a rank
* There **must** be only one contact with a rank of 1
* All contacts **must** have at least one contact method (phone, email, etc.)
* All contact methods **must** have a rank
* There **must** be only one contact method with a rank of 1
* The contact ranked 1 and the contact method ranked 1 **must** be the primary callback for the request
<br>
<br>
### Audit
* Sufficient information around any activity through the API and subsequent BaRS workflow **must** be persisted to aid support incidents and audit requirements
<br>
<br>
### Error Handling 
* Suppliers **must** adhere to the {{pagelink:core-ErrorHandling-1.1.3, text:error handling guidance}} 
<br>
<br>
### Non Functional 
* Suppliers **must** adhere to the {{pagelink:core-NFR-1.1.3, text:non functional requirements}}
<br>
<br>
<hr>