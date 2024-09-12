---
topic: core-content-negotiation-workflow
---

# {{page-title}}

The following sequences give a basic overview of the roles of both the Sender and the Receiver for Content Negotiation:

## CapabilityStatement

The response to the GET /metadata is evaluated by the sender. The normal Version header checks occur. If a CapabilityStatement is returned and all the required items are present for the desired workflow (Version, Functions, MessageDefinitions), the workflow can continue. Else, the Sender should stop.

<a href="https://raw.githubusercontent.com/NHSDigital/booking-and-referral-media/master/src/images/EntityMaps/EntityMapReferralRequest-1.0.0.svg" target="_blank"><img src="https://raw.githubusercontent.com/NHSDigital/booking-and-referral-media/master/src/images/SequenceDiagrams/ContentNegotiation/ContentNegotiation-CapabilityStatement.1.0.0.svg" width="1200"></img></a>

## MessageDefinition

The response to the GET /MessageDefinition is evaluated by the sender. The normal Version header checks occur. If the Message Definition version is acceptable and the use case category and service id match what is expected for the relevant message definition, continue including the use case category in the body of the next request. Else, the Sender should stop. 

<a href="https://raw.githubusercontent.com/NHSDigital/booking-and-referral-media/master/src/images/EntityMaps/EntityMapReferralRequest-1.0.0.svg" target="_blank"><img src="https://raw.githubusercontent.com/NHSDigital/booking-and-referral-media/master/src/images/SequenceDiagrams/ContentNegotiation/ContentNegotiation-MessageDefinition.1.0.0.svg" width="1200"></img></a>


## $process-message

The sending system sends a ServiceRequest/Booking request and the Receiver checks the use case category code to ensure that service can accept it as per the MessageDefinition associated with the service. The normal Version header checks occur.  

<a href="https://raw.githubusercontent.com/NHSDigital/booking-and-referral-media/master/src/images/EntityMaps/EntityMapReferralRequest-1.0.0.svg" target="_blank"><img src="https://raw.githubusercontent.com/NHSDigital/booking-and-referral-media/master/src/images/SequenceDiagrams/ContentNegotiation/ContentNegotiation-process-message.1.0.0.svg" width="1200"></img></a>
