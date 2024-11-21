---
topic: applications
---

## {{page-title}}

Applications are the use of the standard when applied to a particular workflow or care journey. The Application of BaRS describes how particular operations and business flows map to the underlying technical capabilities and patterns of the Core elements of the BaRS along with the specific payloads (the information to be moved).

This page provides a catalogue of implementation guides that have been developed to support specific use cases. These Application specific implementation guides confirm:
- the scope
- any requirements in addition to BaRS Core
- the specific payload for that use case.



These guides are designed to be used in conjunction with the documentation for {{pagelink:design-core-1.0.5}}.



| Application                                                                 |  Use Cases                                                     | Current Release | Minimum API Spec | Minimum Core Version |
| ----------------------------------------------------------------------------|--------------------------------------------------------------- | --------------- | --------------- | --------------- |    
| {{pagelink:application1, text:Booking and Referrals into UEC (Application 1)}}  | <p>111 - ED <br>111 - UTC <br>CAS - ED <br>CAS - UTC <br> 999 - ED <br> 999 - UTC <br> 111 - SDEC <br> CAS - SDEC <br> 999 - SDEC <br> </p> | 1.0.5           | <a href="https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_0_0" target="_blank">v1.0.0</a> | <a href="https://simplifier.net/guide/nhsbookingandreferralstandard/Home/Design/BaRS-Core?version=1.0.0" target="_blank">v1.0.0</a> |
| {{pagelink:application2, text: Booking and Referrals into UEC (Application 2)}} | <p>111 Online - ED <br>111 Online - UTC <br> S&R - ED <br> S&R - UTC <br> <p>               | 1.0.5           | <a href="https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_0_0" target="_blank">v1.0.0</a> | <a href="https://simplifier.net/guide/nhsbookingandreferralstandard/Home/Design/BaRS-Core?version=1.0.0" target="_blank">v1.0.0</a> |
| {{pagelink:application3, text: Referral into UEC (Application 3)}} | <p>999-CAS Referral<br> | 1.0.1     | <a href="https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_0_0" target="_blank">v1.0.0</a> | <a href="https://simplifier.net/guide/nhsbookingandreferralstandard/Home/Design/BaRS-Core?version=1.0.0" target="_blank">v1.0.0</a> |
| {{pagelink:application4, text: Referral into UEC for Validation (Application 4)}} | <p>999-CAS Validation<br> <p>999 AST to Falls Lifting Service<br> <p>999 AST to Community Services <br> | 1.2.0     | <a href="https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_0_0" target="_blank">v1.0.0</a> | <a href="https://simplifier.net/guide/nhsbookingandreferralstandard/Home/Design/BaRS-Core?version=1.0.0" target="_blank">v1.0.0</a> |
| {{pagelink:application5, text: Referrals into Pharmacy (Application 5)}}      | <p>Primary Care to Community Pharmacy (Pharmacy First)<br> <p>Primary Care to Pharmacy Contraception (Oral Contraception) <br> <p>Primary Care to Pharmacy Blood Pressure Check Service<br> | 1.1.0     | <a href="https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_1_0" target="_blank">v1.1.0</a> | {{pagelink:design-core-1.1.5, text:v1.1.0}} |


<hr>

## Versioning Matrix

Table detailing active versions of the latest Applications in Production (or currently being built to) and their supporting Implementation Guide, Core and API versions.

<table>
<thead>
	<tr>
		<th data-no-sort="">Application Version</th>
		<th data-no-sort="">Minimum BaRS Guide Version</th>
		<th data-no-sort="">Minimum Core Version</th>
		<th data-no-sort="">Minimum API Spec version</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>Application 1 v1.0.1</td>
		<td><a href="https://simplifier.net/guide/nhsbookingandreferralstandard/home?version=1.1.0" target="_blank">v1.1.0</a></td>
		<td rowspan=10 style="text-align: center; vertical-align: middle;"><a href="https://simplifier.net/guide/nhsbookingandreferralstandard/Home/Design/BaRS-Core?version=1.0.0" target="_blank">v1.0.0</a></td>
		<td rowspan=10 style="text-align: center; vertical-align: middle;"><a href="https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_0_0" target="_blank">1.0.0</a></td>		
	</tr>
	<tr>
		<td>Application 1 v1.0.3</td>
		<td><a href="https://simplifier.net/guide/nhsbookingandreferralstandard/home?version=1.4.0" target="_blank">v1.4.0</a></td>
	</tr>
	<tr>
		<td>Application 1 v1.0.5</td>
		<td><a href="https://simplifier.net/guide/nhsbookingandreferralstandard/home?version=1.8.0" target="_blank">v1.8.0</a></td>
	</tr>
	<tr>
		<td>Application 2 v1.0.1</td>
		<td><a href="https://simplifier.net/guide/nhsbookingandreferralstandard/home?version=1.1.0" target="_blank">v1.1.0</a></td>
	</tr>
	<tr>
		<td>Application 2 v1.0.3</td>
		<td><a href="https://simplifier.net/guide/nhsbookingandreferralstandard/home?version=1.4.0" target="_blank">v1.4.0</a></td>
	</tr>
	<tr>
		<td>Application 2 v1.0.5</td>
		<td><a href="https://simplifier.net/guide/nhsbookingandreferralstandard/home?version=1.8.0" target="_blank">v1.8.0</a></td>
	</tr>
	<tr>
		<td>Application 3 v1.0.0</td>
		<td><a href="https://simplifier.net/guide/nhsbookingandreferralstandard/home?version=1.4.0" target="_blank">v1.4.0</a></td>
	</tr>
	<tr>
		<td>Application 3 v1.0.1</td>
		<td><a href="https://simplifier.net/guide/nhsbookingandreferralstandard/home?version=1.6.0" target="_blank">v1.6.0</a></td>
	</tr>
	<tr>
		<td>Application 4 v1.0.0</td>
		<td><a href="https://simplifier.net/guide/nhsbookingandreferralstandard/home?version=1.4.0" target="_blank">v1.4.0</a></td>
	</tr>
	<tr>
		<td>Application 4 v1.2.0</td>
		<td><a href="https://simplifier.net/guide/nhsbookingandreferralstandard/home?version=1.8.0" target="_blank">v1.8.0</a></td>
	</tr>
	<tr>
		<td>Application 5 v1.0.0-beta.4</td>
		<td><a href="https://simplifier.net/guide/nhsbookingandreferralstandard/home?version=1.4.0" target="_blank">v1.4.0</a></td>
		<td rowspan=4 style="text-align: center; vertical-align: middle;"><a href="https://simplifier.net/guide/nhsbookingandreferralstandard/Home/Core/End-to-end-workflow?version=1.4.0" target="_blank">v1.1.0</a></td>
		<td rowspan=4 style="text-align: center; vertical-align: middle;"><a href="https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_1_0" target="_blank">1.1.0</a></td>
	</tr>
	<tr>
		<td>Application 5 v1.0.0</td>
		<td><a href="https://simplifier.net/guide/nhsbookingandreferralstandard/home?version=1.7.0" target="_blank">v1.7.0</a></td>
	</tr>
	<tr>
		<td>Application 5 v1.1.0</td>
		<td><a href="https://simplifier.net/guide/nhsbookingandreferralstandard/home?version=1.8.0" target="_blank">v1.8.0</a></td>
	</tr>
	<tr>
		<td>Application 6 v1.0.0-beta.2</td>
		<td><a href="https://simplifier.net/guide/nhsbookingandreferralstandard/home?version=1.8.0" target="_blank">v1.8.0</a></td>
	</tr>
	<tr>
		<td>Application 7 v1.0.0-alpha</td>
		<td><a href="https://simplifier.net/guide/nhsbookingandreferralstandard/home?version=1.8.0" target="_blank">v1.8.0</a></td>
		<td rowspan=1 style="text-align: center; vertical-align: middle;"><a href="https://simplifier.net/guide/nhsbookingandreferralstandard/Home/Design/BaRS-Core?version=1.0.0" target="_blank">v1.0.0</a></td>
		<td rowspan=1 style="text-align: center; vertical-align: middle;"><a href="https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_0_0" target="_blank">1.0.0</a></td>
	</tr>
	<tr>
		<td></td>
		<td></td>
		<td></td>
		<td></td>
	</tr>
</tbody>
</table>

