---
topic: core-SPUseCaseCategories-1.2.2
---

# {{page-title}}

## What are use case categories?

Use case categories define the specific type of referral being requested.  The type is categorised at the service level.  A BaRS Application can support multiple use cases; a use case can only ever belong to one BaRS Application.  For instance, in Application 6 there are three defined use cases: Out of Area, Mutual Aid and Call Assist.  All of these use cases relate to referrals between Ambulance Service Trusts but the workflow, timeframes and responses are not universal across all three scenarios.  

The BaRS use case categories are defined in the BARS CodeSystem (https://simplifier.net/nhsbookingandreferrals/usecases-categories-bars).  All BaRS compliant solutions must adopt use case categories.

## How to use BaRS use case categories

The use case category is used in the initial content negotiation phase:
* when a Sender makes a request for MessageDefinitions and the Receiver responds
* when the Sender makes a referral request to the Receiver

 
When a Sender makes a request for MessageDefinitions, the MessageDefinitions returned by the Receiver will contain a use case category code (from the use case categories code system) under Message.Definition.useContext.code.  The Sender **must** read this field to verify the Receiver supports the use case workflow they require.  The use case category code will also be included in:
* the Sender's service request under ServiceRequest.category
* the Sender’s booking request under Appointment.ServiceCategory

If this is not a use case supported by the Receiver, they will respond with an error (Operation Outcome).
 
The sequence of events occurs as follows:
* the Sender requests the MessageDefinitions 
* the Receiver indicates the use-case categories they support
* the Sender reads and only engages in the use-case workflows supported
* the Sender's request includes the use-case category code (the same code they read from the MessageDefinition), under ServiceRequest.category (referral) or Appointment.ServiceCategory (booking)
* the Receiver processes accordingly








