---
topic: core-StandardPattern-document-reference-Introduction-1.1.3
---

# DocumentReference

<div markdown="span" class="alert alert-warning" role="alert"><i class="fa fa-warning"></i><b>Important:  Release information</b>
<p>This Section of the Implementation Guide is currently a preview, in an Alpha state and subject to change.</p>
</div>

## Introduction

In version 1.1.0 of the BaRS API Specification, functionality was added to accommodate the use of pointers (DocumentReference resources), to locate existing bookings and referrals.

The FHIR DocumentReference resource allows you to reference and locate clinical documents or resources. This section will walk you through the process of using a FHIR DocumentReference to find a resource's location and retrieve it.

The BaRS API acts as a gateway to the National Record Locator FHIR API for BaRS enabled Services. In the image below the BaRS API is interacted with by Consumers and Producers.
* Consumer - Queries the API for existing DocumentReferences for use in finding existing Bookings and Referrals. This is usually a BaRS [Sender](https://simplifier.net/guide/nhsbookingandreferralstandard/Home/Design/BaRS-Core?version=current#Core-functionality-requirements).
* Producer - Posts and maintains DocumentReferences for Bookings and Referrals that they have received. This is invariably the BaRS [Receiver](https://simplifier.net/guide/nhsbookingandreferralstandard/Home/Design/BaRS-Core?version=current#Core-functionality-requirements).

<img src="https://raw.githubusercontent.com/NHSDigital/booking-and-referral-media/master/src/images/DocumentReference/NRLF Via BaRS-1.1.0.svg" width="1200"></img>
