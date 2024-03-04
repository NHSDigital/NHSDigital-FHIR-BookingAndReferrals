# {{page-title}}

BaRS should provide different functionality depending on:

- its {{pagelink:applications, text:Application or use case}}
- whether it acts as a sender or receiver


This list of functionality will expand in later versions of BaRS.

There are requirements in each of the central areas of functionality which every BaRS Application must adopt:

### All

- Provide Capability Statement 
- Read and interpret Capability State 
- Provide Message Definition(s) for a specific service
- Read and interpret Message Definition(s) for a specific service 

### Caching

- The local caching of retrieved metadata (Capability Statements and Message Definitions) requests is permitted to improve performance
- Caching of responses **must <ins>not</ins>** exceed 24 hours (12 hours is recommended)
- There **must** be a mechanism to manually clear the cache

### Booking Sender 

- Request Slots for a specific service
- Make Booking request
- Cancel Booking request 
- Make Rebook request (two open Bookings during this routine)

### Booking Receiver 

- Provide Slots for a specific service 
- Create Booking 
- Cancel Booking 
- Accept Rebook request (two open Bookings during this routine)

### Referral Sender 

- Make Referral request 
- Cancel Referral request 
- Re-request Service Request (revoke current open Referral prior to sending new. Only one active/open Service Request during this routine)

### Referral Receiver

- Create Referral
- Cancel Referral 
- Accept re-request Service Request (revoke current open Referral prior to sending new. Only one active/open Service Request during this routine)


<hr>