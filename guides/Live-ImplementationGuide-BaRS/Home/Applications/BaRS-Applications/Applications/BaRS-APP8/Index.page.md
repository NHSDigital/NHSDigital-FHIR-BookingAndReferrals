---
topic: Application8
---

# Referrals into a broker for Healthcare Service selection (Application 8)

<div markdown="span" class="alert alert-warning" role="alert"><i class="fa fa-warning"></i><b> Important:</b> This guide is currently under development <hr><p> This is a preview of a developing guide for information only. With the exception of those involved in developing solutions for the first of type (private beta), it is not intended to be used until the completed v1.0.0 documentation for this Application is released <p> If you are interested in developing a BaRS compliant solution right now for the use cases covered by this Application, please use the contact form <a href="https://digital.nhs.uk/services/booking-and-referral-standard/enquiry-form" target="_blank">here</a> and the team will be in touch

<p>

<b> Important: Versioning information</b> 
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
		<td>Application 8 v1.0.0-alpha</td>
		<td><a href="https://simplifier.net/guide/nhsbookingandreferralstandard/Home/Core?version=1.11.0" target="_blank">v1.1.x</a></td>
		<td><a href="https://simplifier.net/guide/nhsbookingandreferralstandard/home?version=1.11.0" target="_blank">v1.11.0</td>
		<td><a href="https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1.3.0" target="_blank">v1.1.0</a></td>
	</tr>
</tbody>
</table>

</div>

## Use Cases Supported

This application supports the use of the following use cases:

|Use case                                                                        | Name | Code|
|--------------------------------------------------------------------------------|------|------|
| Advice and Guidance to electronic-Referral Service (e-RS)| AG to e-RS  | A8T1 |
| 111Online to electronic-Referral Service (e-RS)| 111online to e-RS  | A8T2 |
| NHS.UK to electronic-Referral Service (e-RS)| nhs.uk to e-RS  | A8T3 |


## Introduction

### Overview

This page provides guidance for implementing the Referral Standard (BaRS) specifically for the use cases listed above. It should be used alongside the {{pagelink:design-core-1.4.0, text:BaRS Core implementation guide}} and [API Specification](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1.4.0) when developing to the standard. 

### Data model endorsements

NHS England teams within Referrals and Appointments, Digitial Urgent and Emergency Care and the National Pathway for Self-Referrals have co-produced the Application 8 standard to facilitate interoperability between existing systems for referral pathways.  

<hr />