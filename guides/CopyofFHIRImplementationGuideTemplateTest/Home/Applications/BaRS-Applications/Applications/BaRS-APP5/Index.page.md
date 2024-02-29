---
topic: Application5
---

# Referrals into Pharmacy (Application 5)

<div markdown="span" class="alert alert-warning" role="alert"><i class="fa fa-warning"></i><b> Important:</b> This guide is currently under development <hr><p> This is a preview of a developing guide for information only. With the exception of those involved in developing solutions for the first of type (private beta), It is not intended to be used until the completed v1.0.0 documentation for this application is released <p> If you are interested in developing a BaRS compliant solution right now for the use cases covered by this application, please use the contact form <a href="https://digital.nhs.uk/services/booking-and-referral-standard/enquiry-form" target="_blank">here</a> and the team will be in touch.
<p>

<b>Versioning information</b>
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
		<td>Application 5 v1.0.0-beta2</td>
		<td><a href="https://simplifier.net/guide/nhsbookingandreferralstandard/Home/Core/End-to-end-workflow?version=1.4.0" target="_blank">v1.2.1</a></td>
		<td><a href="https://simplifier.net/guide/nhsbookingandreferralstandard/home?version=1.4.0" target="_blank">v1.4.0</td>
		<td><a href="https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_1_0" target="_blank">v1.1.0</a></td>
	</tr>
</tbody>
</table>

</div>



## Use Cases Supported

This application supports the use of the following use cases:

- Primary Care to Community Pharmacy (CPCS)

## Introduction

### Overview

This page provides guidance for implementing the Referral Standard (BaRS) specifically for the use cases listed above. It should be used alongside the {{pagelink:design-core, text:BaRS Core implementation guide}} and Payload Definitions when developing to the standard. 

### Data model endorsements

The GP to Pharmacy CPCS (Community Pharmacist Consultation Service) Minor Illness referral information data model is informed by user research with pharmacy service providers. We have engaged with NHS England (NHSE) Policy teams to establish the service information requirements. The data model is based on the Community Pharmacy Standard v3.0 as defined and endorsed by the Professional Records Standards Body (PRSB). The referral information has been validated by the NHSE Pharmacy Clinical Reference Group. This provides the necessary confidence that solutions built to the standard will be both fit for purpose and safe.

