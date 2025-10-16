---
topic: core-StandardPattern-document-reference-Introduction-1.3.1
---

# Standard Pattern - DocumentReference

<div markdown="span" class="alert alert-warning" role="alert"><i class="fa fa-warning"></i><b>Important:  Release information</b>
<p>This Section of the Implementation Guide is currently a preview, in an Alpha state and subject to change.</p>
</div>

## Introduction

There is functionality in BaRS to accommodate the use of pointers (DocumentReference resources), to locate existing bookings and referrals from a central Registy.

This section will walk you through the process of using FHIR DocumentReferences, from the central Registry, to find and retrieve bookings and referrals held at Receiver services.

The BaRS API acts as a gateway to the National Record Locator (NRL) FHIR API, for BaRS enabled Services. In the image below the BaRS API is called by Consumers and Producers.
* Consumer - Queries the API for existing DocumentReferences for use in finding existing Bookings and Referrals. Usually a BaRS [Sender](https://simplifier.net/guide/nhsbookingandreferralstandard/Home/Core/1.3.0/Core-Functionality-Requirements).
* Producer - Posts and maintains DocumentReferences for Bookings and Referrals that they have received. Usually a BaRS [Receiver](https://simplifier.net/guide/nhsbookingandreferralstandard/Home/Core/1.3.0/Core-Functionality-Requirements).

<img src="https://raw.githubusercontent.com/NHSDigital/NHSDigital-FHIR-BookingAndReferrals/main/BaRS-Images/DocumentReference/NRLF Via BaRS-1.1.0.svg" width="1200"></img>
