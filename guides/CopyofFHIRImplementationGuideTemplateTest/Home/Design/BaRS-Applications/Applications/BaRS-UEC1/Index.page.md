---
topic: app-uec1
---
# Bookings and Referrals into UEC Application 1

## Use Cases Supported

This application supports the use of the following use cases:

* 111 (telephony) to ED (Emergency Department)
* 111 (telephony) to UTC (Urgent Treatment Centre)
* IUC CAS (Integrated Urgent Care Clinical Assessment Service) to ED (Emergency Department)
* IUC CAS (Integrated Urgent Care Clinical Assessment Service) to UTC (Urgent Treatment Centre)

**note:** for use cases where the sending system is 111 Online, please see {{pagelink: app-uec2, text:Bookings and Referrals into UEC Application 2}}

## Introduction

### Overview

This page provides guidance for implementing the Booking and Referral Standard (BaRS) specifically for the NHS 111 (telephony) to Emergency Department (ED, also known as Accident and Emergency or A&E) and Urgent Treatment Centre (UTC) use cases. It should be used alongside the {{pagelink:design-core, text:BaRS Core implementation guide}} and Payload Definitions when developing to the standard. 

### Data model endorsements

<p>
The referral information data model is based on user research with NHS 111 service providers, 999 Ambulance Service Trusts and clinical and administrative Emergency Department staff.  We carried out this research in parallel with the <a href="https://theprsb.org/" target="_blank">Professional Records Standards Body (PRSB)</a> who examined the wider brief of 'referrals from NHS 111 to any other care setting'. 

We worked alongside PRSB to ensure data transferred from 111 to ED is clinically relevant and safe. <a href="https://theprsb.org/standards/111referralstandard/" target="_blank">PRSB have defined and endorsed an information model</a> which works for both the senders (111) and receivers (ED) when referrals are made between the respective services. This endorsement provides the necessary confidence that solutions built to the standard will be both fit for purpose and safe. 
<p>
<hr>
