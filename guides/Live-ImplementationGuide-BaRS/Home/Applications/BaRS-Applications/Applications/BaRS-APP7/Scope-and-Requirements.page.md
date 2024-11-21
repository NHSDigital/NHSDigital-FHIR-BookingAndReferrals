---
topic: APP7-ScopeAndRequirements
---

## {{page-title}}

### Scope Overview
This BaRS Application (Application 7) covers only use case:
* Appointments for Patient Facing Services to GP Practice

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

**API-M**
* All requests and response associated with BaRS must occur through the BaRS API Proxy

**Constraints**

* No additional guidance provided on Slot display for Booking 
* Consent within BaRS will be for Direct-Care only 
* Certificates for Receiving messages to use nhs.uk domains only.
* Receiving endpoints are to be internet facing.
* Limited Search Slot parameters for Booking - Schedule.actor:healthcareService, Start (range), (slot) status
* Clinical Constraints exist - See [Hazard Log](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/onboarding-support-information#downloads)
* No element level 'updates' to requests. A new request must be generated to change information in a booking

### Requirements

**Service Discovery** 
* The service **must** support a unique identifier which the Sender extracts to engage in the booking workflow

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
* Where a national identifier is included, it **must** have a [verification status](https://simplifier.net/hl7fhirukcorer4/valueset-ukcore-nhsnumberverificationstatus) of 'Number present and verified' or 'Number present but not traced', otherwise, the referral Sender **must <ins>not</ins>** include it in the request
* Where the booking was <ins>not</ins> successful, the Receiver **must** send an appropriate response. See {{pagelink:core-failure_scenarios-1.1.5, text:failure scenarios}} for more detail.
* Where the booking was <ins>not</ins> successful, the Sender **must** present an appropriate message to the end user. See {{pagelink:core-failure_scenarios-1.1.5, text:failure scenarios}} for more detail.
* If included in the synchronous HTTP response, the booking Sender **must** make available the human readable identifier for the booking to the end user
* Update to amend a booking request is **<ins>not</ins>** supported. If a booking Sender wishes to change information in a request they **must** follow the re-book workflow

**Cancel booking** 
*	The booking Sender **must** be capable of cancelling any booking made by them, within the current consultation or after the consultation event
*	The booking Sender **must** retrieve the booking to be cancelled from the booking Receiver prior to cancellation to ensure they are working with the most up to date version and it has not already been completed
*	The booking Sender **must** provide visible confirmation to the end user of the status returned by the booking Receiver, indicating whether the original booking was successfully cancelled or not
*	If the cancellation fails the booking Receiver **must** respond with the most appropriately aligned error 
*	The booking Receiver **must** store all previous versions of the booking, including cancellations
*	The booking Receiver **must <ins>not</ins>** be required to inform the patient of the cancellation of the booking.  Business/clinical responsibility for informing the patient must remain with the booking Sender

**Rebook** 
*	The booking Sender **must** be capable of rebooking within the current consultation or after the consultation event
*	Prior to any rebook workflow being attempted, following a previously successful booking, the patient **should** be reassessed 
*	The booking Sender **must** cancel the original booking prior to making the new booking, whether within the current consultation or after the consultation event
*	The booking Sender **must** provide visible confirmation to the end user of the status returned by the Receiver, indicating whether the original booking was successfully cancelled and the new booking made 
*	The booking Receiver **must <ins>not</ins>** be required to inform the patient of the cancellation, incurred as part of the rebooking process. Business/clinical responsibility for informing the patient must remain with the booking Sender

**Contacts** 
* A minimum of one contact (patient or third party) with a contact method (phone, email, etc.) of <ins>phone</ins> **must** be provided in booking requests
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
* Suppliers **must** adhere to the {{pagelink:core-ErrorHandling-1.1.5, text:error handling guidance}} 
<br>
<br>
### Non Functional 
* Suppliers **must** adhere to the {{pagelink:core-NFR-1.1.5, text:non functional requirements}}

<br>
<br>
<hr>