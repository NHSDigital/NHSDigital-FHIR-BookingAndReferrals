---
topic: core-StandardPattern-Endpoint-Sequences-1.2.0
---

# Sequences

The sequences to create, update or read an endpoint via BaRS are detailed below. Though the interaction for a sender to route to a receiver has not changed, the sequence is included. The Sequence is the same for all resources, that being said, due to constraints on the data, there are limits to certain scenarios depending on if a resource would result in being orphaned, or a duplicate entry is being created.

## Sender

Here a Sender is simply sending a request to a receiver using the NHSD-Target-Identifier header.

<a href="https://raw.githubusercontent.com/NHSDigital/NHSDigital-FHIR-BookingAndReferrals/main/BaRS-Images/SequenceDiagrams/EPC-Sequence-Sender-Abstract.svg" target="_blank"><img src="https://raw.githubusercontent.com/NHSDigital/NHSDigital-FHIR-BookingAndReferrals/main/BaRS-Images/SequenceDiagrams/EPC-Sequence-Sender-Abstract.svg" width="1200"></img></a>


## Create

Here a Receiving system is creating a resource related to an endpoint.

<a href="https://raw.githubusercontent.com/NHSDigital/NHSDigital-FHIR-BookingAndReferrals/main/BaRS-Images/SequenceDiagrams/EPC-Sequence-Receiver-Create-Abstract.svg" target="_blank"><img src="https://raw.githubusercontent.com/NHSDigital/NHSDigital-FHIR-BookingAndReferrals/main/BaRS-Images/SequenceDiagrams/EPC-Sequence-Receiver-Create-Abstract.svg" width="1200"></img></a>


## Update

Here a Receiving system is updating a resource related to an endpoint.

<a href="https://raw.githubusercontent.com/NHSDigital/NHSDigital-FHIR-BookingAndReferrals/main/BaRS-Images/SequenceDiagrams/EPC-Sequence-Receiver-Update-Abstract.svg" target="_blank"><img src="https://raw.githubusercontent.com/NHSDigital/NHSDigital-FHIR-BookingAndReferrals/main/BaRS-Images/SequenceDiagrams/EPC-Sequence-Receiver-Update-Abstract.svg" width="1200"></img></a>
