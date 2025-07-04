---
topic: Application4
---

# Referral into UEC for Validation (Application 4)

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
		<td>Application 4 v1.2.3</td>
		<td><a href="https://simplifier.net/guide/nhsbookingandreferralstandard/Home/Core?version=1.8.2" target="_blank">v1.0.x</a></td>
		<td><a href="https://simplifier.net/guide/nhsbookingandreferralstandard/home?version=1.8.2" target="_blank">v1.9.0</td>
		<td><a href="https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1.0.7" target="_blank">v1.0.0</a></td>
	</tr>
</tbody>
</table>
</div>




## Use cases supported

This application supports the use of the following use cases:

| Use Case                                                                                              | Name | Code |
|-------------------------------------------------------------------------------------------------------|------|------|
| 999 Ambulance Service Trust (AST) validation request to Clinical Assessment Service (CAS)             | 999 to CAS Validation | A4T1 |
| 999 AST to Falls Lifting Service - (Application v1.2.0 and above)                                     | 999 to Falls	| A4T2 |
| 999 AST to Community Services (e.g 2-hour Urgent Community Response) - (Application v1.2.0 and above) | 999 to Community Services		| A4T3 |


</br>
</br>

Note: for referral of 999 AST cases with a non-ambulance triage outcome (CAT 5) to a CAS for consultation and treatment and/or onward referral please see {{pagelink:application3}}

## Data model endorsements

The referral information data model is based on user research with NHS 111 service providers, 999 Ambulance Service Trusts, Clinical Assessment Services and clinical and administrative Emergency Department staff.  We carried out this research in parallel with the [Professional Records Standards Body (PRSB)](https://theprsb.org/) who examined the wider brief of 'referrals from NHS 111 to any other care setting' 

For the validation request into a CAS from a 999 AST use case, the data model was endorsed by NHS England following consultation with the [Association of Ambulance Chief Executives (AACE)](https://aace.org.uk/),  National Ambulance Information Group (NAIG), National Ambulance Services Medical Directors' Group (NASMeD) and National Ambulance Digital Leaders Group (NADLG).

The minor extension to the data model to support the secondary use cases was endorsed by the relevant NHSE policy team clinical stakeholders.

For more information see {{pagelink: application4, text:Referral into UEC for Validation (Application 4}} 
<hr />