---
topic: applications
---

## {{page-title}}

Applications are the use of the standard when applied to a particular workflow or care journey. The Application of BaRS describes how particular operations and business flows map to the underlying technical capabilities and patterns of the Core elements of the BaRS along with the specific payloads (the information to be moved).

This page provides a catalogue of implementation guides that have been developed to support specific use cases. These Application specific implementation guides confirm:
- the scope
- any requirements in addition to BaRS Core
- the specific payload for that use case.



These guides are designed to be used in conjunction with the documentation for {{pagelink:design-core}}.



| Application                                                                 |  Use Cases                                                     | Current Release | Minimum API Spec | Minimum Core Version |
| ----------------------------------------------------------------------------|--------------------------------------------------------------- | --------------- | --------------- | --------------- |    
| {{pagelink:application1, text:Booking and Referrals into UEC (Application 1)}}  | <p>111 - ED <br>111 - UTC <br>CAS - ED <br>CAS - UTC <br> 999 - ED <br> 999 - UTC <br> 111 - SDEC <br> CAS - SDEC <br> 999 - SDEC <br> </p> | 1.0.3           | <a href="https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_0_0" target="_blank">v1.0.0</a> | <a href="https://simplifier.net/guide/nhsbookingandreferralstandard/Home/Design/BaRS-Core?version=1.0.0" target="_blank">v1.0.0</a> |
| {{pagelink:application2, text: Booking and Referrals into UEC (Application 2)}} | <p>111 Online - ED <br>111 Online - UTC <br> S&R - ED <br> S&R - UTC <br> <p>               | 1.0.3           | <a href="https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_0_0" target="_blank">v1.0.0</a> | <a href="https://simplifier.net/guide/nhsbookingandreferralstandard/Home/Design/BaRS-Core?version=1.0.0" target="_blank">v1.0.0</a> |
| {{pagelink:application3, text: Referral into UEC (Application 3)}} | <p>999-CAS Referral<br> | 1.0.0     | <a href="https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_0_0" target="_blank">v1.0.0</a> | <a href="https://simplifier.net/guide/nhsbookingandreferralstandard/Home/Design/BaRS-Core?version=1.0.0" target="_blank">v1.0.0</a> |
| {{pagelink:application4, text: Referral into UEC for Validation (Application 4)}} | <p>999-CAS Validation<br> | 1.1.0     | <a href="https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_0_0" target="_blank">v1.0.0</a> | <a href="https://simplifier.net/guide/nhsbookingandreferralstandard/Home/Design/BaRS-Core?version=1.0.0" target="_blank">v1.0.0</a> |

<hr>

## Versioning Matrix

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
		<td rowspan=7 style="text-align: center; vertical-align: middle;"><a href="https://simplifier.net/guide/nhsbookingandreferralstandard/Home/Design/BaRS-Core?version=1.0.0" target="_blank">v1.0.0</a></td>
		<td rowspan=7 style="text-align: center; vertical-align: middle;"><a href="https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_0_0" target="_blank">1.0.0</a></td>		
	</tr>
	<tr>
		<td>Application 1 v1.0.3</td>
		<td><a href="https://simplifier.net/guide/nhsbookingandreferralstandard/home?version=1.4.0" target="_blank">v1.4.0</a></td>
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
		<td>Application 3 v1.0.0</td>
		<td><a href="https://simplifier.net/guide/nhsbookingandreferralstandard/home?version=1.4.0" target="_blank">v1.4.0</a></td>
	</tr>
	<tr>
		<td>Application 4 v1.0.0</td>
		<td><a href="https://simplifier.net/guide/nhsbookingandreferralstandard/home?version=1.4.0" target="_blank">v1.4.0</a></td>
	</tr>
	<tr>
		<td>Application 4 v1.1.0</td>
		<td><a href="https://simplifier.net/guide/nhsbookingandreferralstandard/home?version=1.5.0" target="_blank">v1.5.0</a></td>
	</tr>
	<tr>
		<td>Application 5 v1.0.0-beta3</td>
		<td><a href="https://simplifier.net/guide/nhsbookingandreferralstandard/home?version=1.5.0" target="_blank">v1.5.0</a></td>
		<td rowspan=2 style="text-align: center; vertical-align: middle;"><a href="https://simplifier.net/guide/nhsbookingandreferralstandard/Home/Core?version=1.4.0" target="_blank">v1.1.0</a></td>
		<td rowspan=2 style="text-align: center; vertical-align: middle;"><a href="https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_1_0" target="_blank">1.1.0</a></td>
	</tr>
	<tr>
		<td>Application 6 v1.0.0-beta</td>
		<td><a href="https://simplifier.net/guide/nhsbookingandreferralstandard/home?version=1.5.0" target="_blank">v1.5.0</a></td>
    </tr>
	<tr>
		<td></td>
		<td></td>
		<td></td>
		<td></td>
	</tr>
</tbody>
</table>

