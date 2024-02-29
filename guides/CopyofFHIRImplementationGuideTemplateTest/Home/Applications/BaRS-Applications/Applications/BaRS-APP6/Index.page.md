---
topic: Application6
---

# Referrals into an Ambulance Service Trust (Application 6)


<div markdown="span" class="alert alert-warning" role="alert"><i class="fa fa-warning"></i><b> Important:</b> This guide is currently under development <hr><p> This is a preview of a developing guide for information only. With the exception of those involved in developing solutions for the first of type (private beta), It is not intended to be used until the completed v1.0.0 documentation for this application is released <p> If you are interested in developing a BaRS compliant solution right now for the use cases covered by this application, please use the contact form <a href="https://digital.nhs.uk/services/booking-and-referral-standard/enquiry-form" target="_blank">here</a> and the team will be in touch

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
		<td>Application 6 v1.0.0-beta</td>
		<td><a href="https://simplifier.net/guide/nhsbookingandreferralstandard/Home/Core/End-to-end-workflow?version=1.4.0" target="_blank">v1.2.1</a></td>
		<td><a href="https://simplifier.net/guide/nhsbookingandreferralstandard/home?version=1.4.0" target="_blank">v1.4.0</td>
		<td><a href="https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_1_0" target="_blank">v1.1.0</a></td>
	</tr>
</tbody>
</table>

</div>


## Use Cases Supported

This application supports the use of the following use cases:

*Note: when this application is used for Referrals from an AST Computer Aided Dispatch system (CAD) to an AST CAD it is known as 'CAD to CAD'*

* CAD to CAD Out of Area Referral
* CAD to CAD Call Assist Request
* CAD to CAD Mutual Aid Request

</br>
</br>

## Introduction

### Overview

This page provides guidance for implementing the Referral Standard (BaRS) specifically for the use cases listed above. It should be used alongside the {{pagelink:design-core, text:BaRS Core implementation guide}} and Payload Definitions when developing to the standard. 

</br>
</br>

## Data model endorsements

The referral information data model is based on user research with NHS 111 service providers, 999 Ambulance Service Trusts, Clinical Assessment Services and clinical and administrative Emergency Department staff.  We carried out this research in parallel with the [Professional Records Standards Body (PRSB)](https://theprsb.org/) who examined the wider brief of 'referrals from NHS 111 to any other care setting' 

For the CAD to CAD use case, the data model was agreed by the CAD to CAD Reference Group following a period of user research involving site visits, Reference Group workshops and desk research. This was endorsed by the CAD to CAD Working Group and shared with the the following organisations:

* National Ambulance Programme Board (NAPB)
* National Ambulance Advisory Group (NAAG)
* National Ambulance Information Group (NAIG)
* National Ambulance Services Medical Directors' Group (NASMeD)
* National Ambulance Digital Leaders Group (NADLG)
* National Heads of EOC Group (NHoEOC)
* National Information Governance Group
* National Directors of Operations Group (NDOG)

<hr>