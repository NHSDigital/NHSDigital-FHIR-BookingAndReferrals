---
topic: Application5
---

# Referrals into Pharmacy (Application 5)

 <div markdown="span" class="alert alert-warning" role="alert"><i class="fa fa-warning"></i><b> Important: Versioning information</b> 
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
		<td>Application 5 v1.1.1</td>
		<td><a href="https://simplifier.net/guide/nhsbookingandreferralstandard/Home/Core?version=1.8.0" target="_blank">v1.1.0</a></td>
		<td><a href="https://simplifier.net/guide/nhsbookingandreferralstandard/home?version=1.8.0" target="_blank">v1.8.1</td>
		<td><a href="https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_1_0" target="_blank">v1.1.0</a></td>
	</tr>
</tbody>
</table>

</div>



## Use Cases Supported

This application supports the use of the following use cases:

| Use Case                                                                                                                                                                      | Name |  Code |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------|-------|
| Deprecated -  Primary Care to Community Pharmacy (Pharmacy First)                                                                                                                 | Primary Care to Community Pharmacy | referraltopharmacy |
| Primary Care to Community Pharmacy (Pharmacy First)                                                                                                                           | Primary Care to Community Pharmacy| A5T1 |
| Primary Care to Pharmacy Contraception (Oral Contraception for supply of initial or repeat prescriptions for Combined Oral Contraceptive (COC) or Proestogen Only Pill (POP)) | Primary Care to Pharmacy Contraception | A5T2 |
| Primary Care to Pharmacy Blood Pressure Check Service                                                                                                                         | Primary Care to Pharmacy Blood Pressure Check Service | A5T3 |


NB - 'Primary Care' currently includes GP Practice and Online Consultation, as described in the [BaRS Clinical Safety Case Report (CSCR)](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/onboarding-support-information#downloads)

## Introduction

### Overview

This page provides guidance for implementing the Referral Standard (BaRS) specifically for the use cases listed above. It should be used alongside the {{pagelink:design-core-1.0.5, text:BaRS Core implementation guide}} and Payload Definitions when developing to the standard. 

### Data model endorsements

The GP to Pharmacy (Pharmacy First) Minor Illness referral information data model is informed by user research with pharmacy service providers. We have engaged with NHS England (NHSE) Policy teams to establish the service information requirements. The data model is based on the Community Pharmacy Standard v3.0 as defined and endorsed by the Professional Records Standards Body (PRSB). The referral information has been validated by the NHSE Pharmacy Clinical Reference Group. This provides the necessary confidence that solutions built to the standard will be both fit for purpose and safe.

For more information see {{pagelink: application5, text:Referrals into Pharmacy (UEC Application 5}} 
<hr />