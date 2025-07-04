---
topic: core-EndToEndWorkflow-Logging-1.3.0
---

## {{page-title}}

<div markdown="span" class="alert alert-warning" role="alert"><i class="fa fa-warning"></i><b> Important:  Versioning information - Preview</b> </div>
<p>

| Header                 | Requirement            | Description                                                  | Value                      |
|------------------------|------------------------|--------------------------------------------------------------|----------------------------|
| use-context | Required by the sender | Allows BaRS to route the message to the appropriate endpoint | Formatted string |

This header is for usage statistics for the BaRS Proxy for NHS England. It consists of a composite of 4 values from within the payload, in order. The sender MUST include this information. The receiver MUST ignore this header. The elements are:

The elements for a ServiceRequest are:

* ServiceRequest.category.coding.code (usecases-categories-bars)
* ServiceRequest.category.coding.code (message-category-servicerequest)
* MessageHeader.eventCoding.code (message-event-bars)
* MessageHeader.reason.coding.code (message-reason-bars)

The elements for an Appointment are:

* Appointment.serviceCategory.coding (usecases-categories-bars)
* Appointment.status
* MessageHeader.eventCoding.code (message-event-bars)
* MessageHeader.reason.coding.code (message-reason-bars)

These MUST be present in the use-context header, separated by a pipe, in the defined order.

### Referral

```
ServiceRequest.category.coding.code[usecases-categories-bars] | ServiceRequest.category.coding.code[message-category-servicerequest] | MessageHeader.eventCoding.code | MessageHeader.reason.coding.code 
```
Example:
```
--header 'use-context: a4t2|validation|servicerequest-response|new'
```

### Booking

```
 Appointment.serviceCategory.coding[usecases-categories-bars] | Appointment.status | MessageHeader.eventCoding.code | MessageHeader.reason.coding.code 
```
Example:
```
--header 'use-context: a1t1|booked|booking-request|new'
```

This header is applicable to the following endpoints:
 * POST /$process-message
 * POST /Appointment
 * PUT /Appointment/{id}
 * PATCH /Appointment/{id}
 * POST /ServiceRequest
 * PUT /ServiceRequest/{id}
 * PATCH /ServiceRequest/{id}
 
<hr>
<br>