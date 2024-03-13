---
topic: Application1
---

# Bookings and Referrals into UEC Application 1


<div markdown="span" class="alert alert-warning" role="alert"><i class="fa fa-warning"></i><b> Important:  Versioning information</b>
<p>

<table>
<thead>
	<tr>
		<th data-no-sort="">Application Version</th>
		<th data-no-sort="">Minimum Core Version</th>
		<th data-no-sort="">Minimum Guide Version</th>
		<th data-no-sort="">Minimum API Spec Version</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>Application 1 v1.0.3</td>
		<td><a href="https://simplifier.net/guide/nhsbookingandreferralstandard/Home/Design/BaRS-Core?version=1.0.0" target="_blank">v1.0.0</a></td>
		<td><a href="https://simplifier.net/guide/nhsbookingandreferralstandard/home?version=1.1.0" target="_blank">v1.1.0</td>
		<td><a href="https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_0_0" target="_blank">v1.0.0</a></td>
	</tr>
</tbody>
</table>
</div>



## Use Cases Supported

This Application supports the use of the following use cases:

* 111 (telephony) to ED (Emergency Department)
* 111 (telephony) to UTC (Urgent Treatment Centre)
* IUC CAS (Integrated Urgent Care Clinical Assessment Service) to ED (Emergency Department)
* IUC CAS (Integrated Urgent Care Clinical Assessment Service) to UTC (Urgent Treatment Centre)
* AST (999 Ambulance Service Trust) to ED (Emergency Department)
* AST (999 Ambulance Service Trust) to  UTC (Urgent Treatment Centre)
* 111 (telephony) to SDEC (Same Day Emergency Care)
* IUC CAS (Integrated Urgent Care Clinical Assessment Service) to SDEC (Same Day Emergency Care)
* AST (999 Ambulance Service Trust) to SDEC (Same Day Emergency Care)

**note:** for use cases where the sending system is 111 Online, please see {{pagelink: application2, text:Bookings and Referrals into UEC Application 2}}

## Introduction

### Overview

This page provides guidance for implementing the Booking and Referral Standard (BaRS) specifically for the use cases listed above. It should be used alongside the {{pagelink:design-core, text:BaRS Core implementation guide}} and Payload Definitions when developing to the standard.

### Data model endorsements

<p>
The referral information data model is based on user research with NHS 111 service providers, 999 Ambulance Service Trusts (AST) and clinical and administrative Emergency Department staff.  We carried out this research in parallel with the <a href="https://theprsb.org/" target="_blank">Professional Records Standards Body (PRSB)</a> who examined the wider brief of 'referrals from NHS 111 to any other care setting'. 

We worked alongside PRSB to ensure data transferred from 111 to ED is clinically relevant and safe. <a href="https://theprsb.org/standards/111referralstandard/" target="_blank">PRSB have defined and endorsed an information model</a> which works for both the senders (111) and receivers (ED) when referrals are made between the respective services. This endorsement provides the necessary confidence that solutions built to the standard will be both fit for purpose and safe. 
<p>
<hr>
