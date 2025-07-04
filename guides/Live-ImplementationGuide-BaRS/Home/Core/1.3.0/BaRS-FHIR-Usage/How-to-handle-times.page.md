---
topic: core-FHIRUsage-Time-1.3.0
---

## {{page-title}}

* All times MUST be in FHIR Instant format (```YYYY-MM-DDThh:mm:ss.sssssss+zz:zz```) 
  * e.g. ```Year-Month-DayTHours:Minutes:Seconds.milliseconds+OffsetFromUTC``` 
  * e.g. ```2015-02-07T13:28:17.2398742+02:00```
  * *except* where specifically defined otherwise
* All times can have up to seven digits resolution for milliseconds
* All times SHOULD be converted to UTC from local times (if not stored locally in UTC) before being included in any messages, this means the offset should be zero
* When receiving a time in a message a system MUST expect and handle a non UTC time (e.g. with a non-zero offset)
  * Therefore if a time is received that is not UTC, the receiver should convert the time back to UTC using the offset given (or to their local time, if storing times in a local time)

<div markdown="span" class="alert alert-warning" role="alert"><i class="fa fa-warning"></i><b> Important:</b> 
This means both Sender and Receiver systems MUST be able to handle a time provided with an offset from UTC that differs from your local server time. As an illustration, if you store all times in UTC and someone uses a time specifying an offset, you will need to convert it to UTC when you store it.
</div>