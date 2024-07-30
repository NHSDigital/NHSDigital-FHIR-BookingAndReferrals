---
topic: APP7-ScopeAndRequirements
---

## {{page-title}}

### Scope Overview
This BaRS Application (Application 1) covers only use cases:
* 111 (telephony) to ED
* 111 (telephony) to UTC
* IUC CAS to ED
* IUC CAS to UTC
* AST to ED (Pathways only)
* AST to UTC (Pathways only)
* 111 to SDEC
* CAS to SDEC
* AST to SDEC (Pathways only)

The payloads and workflow have been designed to support these services. Other {{pagelink:applications, text:BaRS Applications}} offer scope for alternative use cases.

### Functional Scope
**Service Discovery**
* Establishing a service to direct requests to is a mandatory step in the workflow
* There is no restriction on the service discovery tools used. Any are capable of being supported whether national or proprietary
* The service **must** be configured within the BaRS infrastructure (Endpoint Catalogue) before requests can be made 

**Slot Management**
* Booking slots are the responsibility and ownership of Receivers to maintain and offer to Senders
* All slot requests **must** occur in real-time without caching by either Senders or Receivers
* The returned slots **should** contain sufficient information for Senders to know what they are booking i.e. have a clear 'type', indicate the role and/or gender of the individual performing on behalf of the service, within any given slot

**Booking**
* Allowing bookings for a service is a method of managing capacity 
* A booking may indicate the exact time an individual can expect to be seen by or is expected to arrive at the service, as is traditionally understood when an 'appointment' is made. Alternatively, the booking timeframe could indicate a range through which the individual may be seen by the service
* The slot the booking is made against may also indicate the type of booking e.g. face-to-face or over the phone and the role of the person who will engage with the individual on behalf of the service
* Bookings are an administrative aspect of the workflow and **should <ins>not</ins>** contain clinically pertinent information

**Referral**
* A referral is a request for care on behalf of an individual from one service to another 
* The referral can be sent without having to establish the capacity the service offers
* The referral will contain primarily clinical information, indicating the need of the individual and **should** state the anticipated action required by the Receiving service
* A referral can be made independent of booking but, where a booking is made as part of the same workflow, they **must** be linked
* Supporting information, other than the assessment, is expected to be included in a referral, if collected, including:
    * new or existing safeguarding concerns
    * locally held Special Patient Notes
    * external information sources used during initial assessment prior to referral
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
* No element level 'updates' to requests. A new request must be generated to change information in a booking or referral request


### Requirements

**Service Discovery** 
* The service **must** support a unique identifier which the Sender extracts to engage in booking and referral workflows

**Slot display** 
* The schedule and related slot(s) **must** contain the actual geographic location (e.g address) of the booking, rather than generic details of the location of the overall service provider.
* The slot **must** contain details of the start/end times of the available slots
* The available slot(s) **must** be capable of being retrieved from any booking Receiver, regardless of the relationship that the sending user’s organisation has with the receiving service 
* Where there are no available slots, the booking Receiver **must** send an appropriate response to indicate this **<ins>not</ins>** merely reply with an empty response
* Where there are no available slots, the booking Sender **must** present an appropriate message to the end user
* The booking Receiver **must** return available slots without requiring to know the potential patient details
* Where the booking Receiver has a number of schedules available to fulfil a request (say, when 2 or more clinicians are delivering surgeries at the same site) they **must** return all of those slots as part of the initial response
* If provided, in addition to Healthcare Service, Schedule and Slot, the booking Sender **must** display Delivery Channel and Practitioner Role, Name and Gender
* Booking Receivers **must <ins>not</ins>** default the Delivery Channel value
* A booking Sender **must <ins>not</ins>** assume a booking Receiver will return requested \_includes e.g. Location
  * Booking Sender **must** handle a Slot response without non mandatory FHIR resources 
  * Booking Sender **must** handle a Slot response with FHIR resources not requested

**Booking** 
* The booking Receiver **must** accept the booking request regardless of whether the patient is known to the service provider
* The booking Receiver **must** accept potential patients who do **<ins>not</ins>** have a national validated identifier e.g. NHS Number.
* Where a national identifier is included, it **must** be 'traced and verified', otherwise, the referral Sender **must <ins>not</ins>** include the national indentifier in the request
* Where the booking was <ins>not</ins> successful, the Receiver **must** send an appropriate response. See {{pagelink:core-failure_scenarios-1.1.3, text:failure scenarios}} for more detail.
* Where the booking was <ins>not</ins> successful, the Sender **must** present an appropriate message to the end user. See {{pagelink:core-failure_scenarios-1.1.3, text:failure scenarios}} for more detail.
* If included in the synchronous HTTP response, the booking Sender **must** make available the human readable identifier for the booking to the end user
* The booking Sender **must** send accompanying clinical information in a BaRS referral request
  * The booking Sender **must** reference the booking in the BaRS referral request (where the booking is made first in the workflow)
  * The booking Receiver **must** link the explicitly related booking and referral requests 
* Update to amend a booking request is **<ins>not</ins>** supported. If a booking Sender wishes to change information in a request they **must** follow the re-book workflow

**Cancel booking** 
*	The booking Sender **must** be capable of cancelling any booking made by them, within the current consultation or after the consultation event
*	The booking Sender **must** retrieve the booking to be cancelled from the booking Receiver prior to cancellation to ensure they are working with the most up to date version and it has not already been completed
*	The booking Sender **must** provide visible confirmation to the end user of the status returned by the booking Receiver, indicating whether the original booking was successfully cancelled or not
*	If the cancellation fails the booking Receiver **must** respond with the most appropriately aligned error 
*	The booking Receiver **must** store all previous versions of the booking, including cancellations
*	The booking Receiver **must <ins>not</ins>** be required to inform the patient of the cancellation of the booking.  Business/clinical responsibility for informing the patient must remain with the booking Sender
*	Any referral, sent as part of a booking, **should** be decoupled from the booking when cancelled and not be assumed to be a referral in its own right i.e. to ensure  'booking only' services are appropriately updated

**Rebook** 
*	The booking Sender **must** be capable of rebooking within the current consultation or after the consultation event
*	If a callback occurs after the consultation has been completed, prior to attempting a rebook the patient **should** be reassessed 
*	The booking Sender **must** cancel the original booking prior to making the new booking, whether within the current consultation or after the consultation event
*	The booking Sender **must** provide visible confirmation to the end user of the status returned by the Receiver, indicating whether the original booking was successfully cancelled and the new booking made 
*	The booking Receiver **must <ins>not</ins>** be required to inform the patient of the cancellation, incurred as part of the rebooking process. Business/clinical responsibility for informing the patient must remain with the booking Sender
*   The new booking **must <ins>not</ins>** link to any originally linked referral, rather a new referral **must** be made and the original 'revoked'

**Booking outside assessment outcome timeframe** 
* The booking Sender **must** allow clinical users to book outside the assessment outcome timeframe
* The booking Sender **must** present a notification to non-clinical users and prompt to seek clinical approval to book outside the assessment outcome timeframe
* The booking Sender **must** store sufficient audit information to show where a patient has been booked outside their assessment outcome timeframe

**Referral requires booking (Require-Booking services)** 
* The booking Sender **must** stop the end users from making a referral if no booking has been made when the “RequireBooking” service attribute is present against the DoS service
* The booking Sender **must** present an appropriate warning message to the end user, indicating the specific service requirements
* The booking Sender **must** allow the referral to be sent when a booking is made
* The end user **must** be allowed to select an alternative service, if they are unable to proceed with "RequireBooking" service

**Referral** 
* The referral Receiver **must** accept the referral request regardless of whether the patient is known to the service provider
* The referral Receiver **must** accept potential patients who do **<ins>not</ins>** have a national validated identifier e.g. NHS Number.
* Where a national identifier is included, it **must** be 'traced and verified', otherwise, the referral Sender **must <ins>not</ins>** include in the request
* Any new or existing safeguarding concern, recorded as part of the assessment, **must** be included in the referral Sender's request
* The referral Receiver **must** clearly identify any included safeguarding concern to the end user
* The referral Receiver **must** accurately represent information made by the Sender to the end user
* The referral Sender **must** make available the human readable identifier for the referral, included in the HTTP synchronous response, to the end user
* Where the referral was <ins>not</ins> successful, the Receiver **must** send an appropriate response. See {{pagelink:core-failure_scenarios-1.1.3, text:failure scenarios}} for more detail.
* Where the referral was <ins>not</ins> successful, the Sender **must** present an appropriate message to the end user. See {{pagelink:core-failure_scenarios-1.1.3, text:failure scenarios}} for more detail.
* The referral Sender **must** include reference to any accompanying BaRS booking related to the referral
  * The referral Sender's request **must** be referenced in the BaRS booking request (where the referral is made first in the workflow)
  * The referral Receiver **must** link the explicitly related booking and referral requests
* Update to amend a referral request is <ins>not</ins> supported. If a referral Sender wishes to change information in a request they **must** follow the re-refer workflow

**Cancel referral** 
*	The referral Sender **must** be capable of cancelling any referral made by them, within the current consultation or after the consultation event
*	The referral Sender **must** retrieve the referral to be cancelled from the referral Receiver prior to cancellation to ensure they are working with the most up-to date version and it has not already been completed
*	The referral Sender **must** provide visible confirmation to the end user of the status returned by the referral Receiver, i.e. whether the original referral was successfully cancelled or not
*	If the update fails the referral Receiver **must** respond with the most appropriately aligned error 
*	The referral Receiver **must** store all previous versions of the referral
*	The referral Receiver **must <ins>not</ins>** be required to inform the patient of the cancellation of the referral.  Business/clinical responsibility for informing the patient must remain with the referral Sender
*	Any booking, sent as part of a referral, **should** be decoupled from the referral when cancelled. It **may** be linked in any subsequent re-refer workflow

**Re-refer** 
*	The referral Sender **must** be capable of re-referring within the current consultation or after the consultation event
*	If a callback occurs, after the consultation has been completed, prior to attempting a re-refer the patient **should** be reassessed 
*	The referral Sender **should** revoke the original referral prior to making a new re-referral, whether within the current consultation or after the consultation event
*	The referral Sender **must** provide visible confirmation to the end user of the status returned by the Receiver, i.e. whether the original referral was successfully revoked and the new referral made 
*	The referral Receiver **must <ins>not</ins>** be required to inform the patient of the cancellation, incurred as part of the re-refer process.  Business/clinical responsibility for informing the patient must remain with the referral Sender

**Contacts** 
* A minimum of one contact (patient or third party) with a contact method (phone, email, etc.) of <ins>phone</ins> **must** be provided in booking and referral requests
* All contacts **must** have a rank associated with them
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