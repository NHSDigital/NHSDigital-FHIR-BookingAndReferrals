---
topic: core-StandardPattern-Endpoint-Introduction-1.2.1
---

<div markdown="span" class="alert alert-warning" role="alert"><i class="fa fa-warning"></i><b> Important:  Versioning information - Preview</b>
<p>

This version of core is strictly a preview of what is currently in development for 1.2.0 and should <b>not be built against.</b>

<table>
<thead>
	<tr>
		<th data-no-sort="">Core Version</th>
		<th data-no-sort="">Minimum Guide Version</th>
		<th data-no-sort="">Minimum API Spec Version</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td><a href="https://simplifier.net/guide/nhsbookingandreferralstandard/Home/Design/BaRS-Core?version=1.0.0" target="_blank">v1.2.0-alpha</a></td>
		<td><a href="https://simplifier.net/guide/nhsbookingandreferralstandard/home?version=1.1.0" target="_blank">v1.8.0</td>
		<td><a href="https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_0_0" target="_blank">v1.2.0</a></td>
	</tr>
</tbody>
</table>
</div>

# Standard Pattern - Endpoints

BaRS employs an endpoint catalogue to match Target Identifiers with a stored endpoint. Target Identifiers are provided in a header which is descripted in the [API Spec](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_2_0) The following pages will describe how these entries can be managed, outside of the onboarding process.

The BaRS endpoints will utilise not only service ids and a physical endpoint, but data describing the healthcare service, the provider of that service and the organization which manages and/or supplies the endpoint in question. This information will be stored using 3 FHIR resources which appropriately describe [Endpoints](http://hl7.org/fhir/R4/endpoint.html), [HealthcareServices](http://hl7.org/fhir/R4/healthcareservice.html) and [Organizations](http://hl7.org/fhir/R4/organization.html).

BaRS will expose an interface to manage this information for each of these resources. Each resource will have a corresponding endpoint on the Proxy to assist in managing these endpoints.