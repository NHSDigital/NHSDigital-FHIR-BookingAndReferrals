---
topic: APP5-HowDoesItWork
---

## {{page-title}}

This section describes how the primary operations used in this application work. This diagram illustrates the workflow and interactions of a referral request:
<br>

<img src="https://raw.githubusercontent.com/NHSDigital/booking-and-referral-media/master/src/images/WorkFlows/GPtoPharmacyCPCS-1.0.0-beta.1.svg" width="1500"></img></a>


To support the workflows for this application of the standard the operations that need to be supported are:

<hr>

### Find a Service

The BaRS referral process as shown above does not include guidance on how a user should determine if a referral to Pharmacy is appropriate for the patient.  It is the responsibility of the referring organisaton to ensure patients are pre-screened by GP Practice staff (care navigators or clinicians) prior to beginning the referral process, using their own judgement or an appropriate triage tool.  

#### Directory of Services API

Pharmacy services are profiled on the <a href="https://digital.nhs.uk/services/directory-of-services-dos" target="_blank">Directory of Services (DoS).</a>

For this application, systems should use the <a href="https://digital.nhs.uk/developer/api-catalogue/directory-of-services-urgent-and-emergency-care-rest" target="_blank">Directory of Services - Urgent and Emergency Care - REST API.</a>

Details on how to develop to use this API and onboard to use it in production, are provided in the links above.

For this application the Service Type search will be used:
<a href="https://developer.nhs.uk/apis/dos-api/byServiceType.html" target="_blank">Search by Service Type | docs-dos-api (developer.nhs.uk).</a>


#### Guidance on how to call the DoS API

This API supports a search by location (e.g. the patient's current location).  Note that the DoS API used does not support the concept of searching for services that are open within a given timeframe, however the results from DOS include all opening times. The service search results should be filtered to those that are open in the timeframe required for the referral.  The filtered results should be displayed back to the user, in order to allow them to choose with the patient where they want to go.

The search parameters to be used are as follows:
<p>

<div class="nhsd-m-emphasis-box">
    <div class="nhsd-a-box nhsd-a-box--border-grey">
        <div class="nhsd-m-emphasis-box__content-box">
            <table>
                <thead>
                    <tr>
                        <th>Parameter</th>
                        <th>Type</th>
                        <th>Required?</th>
						<th>GP to Pharamcy Guidance Notes</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>caseID</td>
                        <td>String</td>
                        <td>No</td>
                        <td>Do not populate</td>
                    </tr>
                    <tr>
                        <td>postcode</td>
                        <td>String</td>
                        <td>Yes</td>
                        <td>Populate with where the GP Practice is or the Patient’s home address – dependent on where the patient is now</td>
                    </tr>
                    <tr>
                        <td>searchDistance</td>
                        <td>Integer</td>
                        <td>No</td>
                        <td>Do not populate – the default value is 37.5 miles which is more than adequate search radius</td>
                    </tr>
                    <tr>
                        <td>gpPracticeID</td>
                        <td>Integer</td>
                        <td>No</td>
                        <td>Do not populate</td>
                    </tr>
                    <tr>
                        <td>age</td>
                        <td>Integer</td>
                        <td>No</td>
                        <td>Do not populate</td>
                    </tr>
                    <tr>
                        <td>gender</td>
                        <td>String</td>
                        <td>No</td>
                        <td>Do not populate</td>
                    </tr>
                    <tr>
                        <td>disposition</td>
                        <td>String</td>
                        <td>No</td>
                        <td>Do not populate</td>
                    </tr>
                    <tr>
                        <td>serviceTypeIds</td>
                        <td>Array</td>
                        <td>Yes</td>
                        <td>Use the relevant service type for the need required in the referral – as detailed further in next section</td>
                    </tr>
                    <tr>
                        <td>numberPerType</td>
                        <td>Integer</td>
                        <td>No</td>
                        <td>Do not populate</td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</div>

<p>


#### Guidance on service search and which services to display 

<div class="nhsd-m-emphasis-box">
    <div class="nhsd-a-box nhsd-a-box--border-grey">
        <div class="nhsd-m-emphasis-box__content-box">
            <table>
                <thead>
                    <tr>
                        <th>Pharmacy Service Type</th>
                        <th>Search method</th>
						<th>Opening Hours Guidance</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>Community Pharmacy Consultation Service and Common Conditions Service</td>
                        <td><b>Use Service Type ID 131- Pharmacy Urgent Meds Supply</b><br>Note this is labelled 'Pharmacy Urgent Meds Supply', but it is deemed appropriate to return one profile per Pharmacy that will do Pharmacy Urgent Meds Supply, CPCS and CCS.</br></td>
                        <td>These services are time critical and the patient must be seen within 24 hours, and so any pharmacies closed now (or closing in the next 30 mins) <b>AND</b> not open in the next 24 hours should not be displayed to the user.<br>Discretion is permitted if the nearest pharmacy is open now but due to close soon.</br><br>If no pharmacies in the local area are open in the next 24 hours then a message needs to be clearly displayed to the user so they can consider other alternatives.  (Note this is a very unlikely scenario – but may happen in rural areas with only a few nearby Pharmacies or around bank holiday weekends).</br><br>Ensure the display clearly shows:</br><li>The opening times, to allow the user to provide opening times to the patient so that they can go to the pharmacy when it is open.</li><li>The phone number for the pharmacy; the user can give this to the patient so they can call and pre-arrange when to come in.</li>
</td>
                    </tr>
                    <tr>
                        <td>Blood Pressure Check Service</td>
                        <td><b>Use Service Type ID 149 - Pharmacy Blood Pressure Check</b></td>
                        <td>This service is not time critical and so all nearest services can be displayed to the user.<br>Ensure the display clearly shows:</br><li>The opening times, to allow the user to provide opening times to the patient so that they can go to the pharmacy when it is open.</li>
<li>The phone number for the pharmacy, so the user can give this to the patient in case they want to call and pre-arrange when to come in.</li>
						</td>
                    </tr>
					<tr>
                        <td>Pharmacy Contraception Service</td>
                        <td><b>Use Service Type ID 149 - Pharmacy Contraception</b></td>
                        <td>This service is not time critical and so all nearest services can be displayed to the user.<br>Ensure the display clearly shows:</br><li>The opening times, to allow the user to provide opening times to the patient so that they can go to the pharmacy when it is open.</li>
<li>The phone number for the pharmacy, so the user can give this to the patient in case they want to call and pre-arrange when to come in.</li>
						</td>
                    </tr>
				</tbody>
            </table>
        </div>
    </div>
</div>

<p></p>

<p>

When a service is chosen, the "Service ID" field in the DOS data will be used as the Receiver Service Identifier to then initiate the referral as per the following sections.
</p>

### Make a Referral

Making a referral for this application follows the {{pagelink:core-standardpattern, text:standard pattern for BaRS operations}}.

The message definition that defines this payload for this application is: {{link:MessageDefinition-BARS-MessageDefinition-ServiceRequest-Request-Referral}}
<p>

<hr>

In addition to that the specific workflow parameters that are required are as follows:

<div class="nhsd-m-emphasis-box">
    <div class="nhsd-a-box nhsd-a-box--border-grey">
        <div class="nhsd-m-emphasis-box__content-box">
            <table>
                <thead>
                    <tr>
                        <th>Interaction</th>
                        <th>Method</th>
                        <th>Payload Focus  </th>
                        <th>Status Required (MessageHeader, ServiceRequest, Encounter)</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td rowspan=6>Referral Request (New)</td>
                        <td rowspan=6>POST /$process-message{servicerequest-request}</td>
                        <td rowspan=6>ServiceRequest (active)</td>
                        <td>MessageHeader (EventCoding) = servicerequest-request</td>
                    </tr>
                    <tr>
                        <td>MessageHeader (ReasonCode) = new</td>
                    </tr>
                    <tr>
                        <td>ServiceRequest (Status) = active</td>
                    </tr>
                    <tr>
                        <td>ServiceRequest (Category) = referral</td>
                    </tr>
					<tr>
                        <td>ServiceRequest (Category) = referraltopharmacy</td>
                    </tr>
                    <tr>
                        <td>Encounter (Status) = triaged/finished</td>
                    </tr>
                    <tr>
                        <td><b>All resources to include 'lastUpdated' value, under meta section</b></td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</div>

<p>

Additionally the HTTP request header would be:

```
NHSD-Target-Identifier = {Receiver Service Identifier}
X-Request-Id = <GUID_000001>
X-Correlation-Id = <GUID_000002>
NHSD-End-User-Organisation = {FHIR Organisation (Base64 Encoded)}
NHSD-Requesting-Practitioner = {FHIR Practitioner (Base64 Encoded)} 
NHSD-Requesting-Software =  {FHIR Device (Base64 Encoded)}
```

The HTTP response header would be:

```
X-Request-Id = <GUID_000001>
X-Correlation-Id = <GUID_000002>
```

### Cancel a Referral

To cancel a referral this application follows the {{pagelink:core-standardpattern, text:standard pattern for BaRS operations}} with an additional step. Before beginning the standard pattern as descbribed on the linked section, the referral **sender** must perform a read of the referral to be cancelled, from the referral **receiver**, prior to cancellation to ensure they are working with the most up-to date information and it has not already been actioned. This is done by performing a "GET ServiceRequest by ID" call to the **receiving** system's corresponding API endpoint (via the BaRS proxy).

The response to this request will be the requested ServiceRequest resource which should be checked for its current status to ensure it does not already have a status of "revoked" or "completed". If not, this version of the ServiceRequest should be used when re-submitting the modified resource in the POST bundle as described in the {{pagelink:core-standardpattern, text:standard pattern}}.

The message definition that defines this payload for this application is: {{link:messagedefinition-barsmessagedefinitionservicerequestrequestcancelled}}

As a general principle, when performing an update type of operation (of which cancellation is a special case), only the focus resource, any resources that are mandated due to contextual, linking or referential integrity reasons and any resources that include elements that are being changed, **should** be include. This is always defined within the relevent message definition.

If the update-to-cancel is taking place as part of a re-referral routine, once the cancellation is complete, the new referral message can be sent. This step in the workflow would follow the same process as 'Make a referral' detailed above.

In addition the specific workflow parameters that are required are as follows:

<div class="nhsd-m-emphasis-box">
    <div class="nhsd-a-box nhsd-a-box--border-grey">
        <div class="nhsd-m-emphasis-box__content-box">
            <table>
                <thead>
                    <tr>
                        <th>Interaction</th>
                        <th>Method</th>
                        <th>Payload Focus  </th>
                        <th>Status Required (MessageHeader, ServiceRequest, Encounter)</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>Get Referral</td>
                        <td>GET /ServiceRequest{id}</td>
                        <td>n/a</td>
                        <td>n/a</td>
                    </tr>
                    <tr>
                        <td rowspan=8>Referral Request (Cancel)</td>
                        <td rowspan=8>POST /$process-message{servicerequest-request}</td>
                        <td rowspan=8>ServiceRequest (revoked)</td>
                        <td>MessageHeader (EventCoding) = servicerequest-request</td>
                    </tr>
                    <tr>
                        <td>MessageHeader (ReasonCode) = update</td>
                    </tr>
                    <tr>
                        <td>ServiceRequest (Status) = revoked</td>
                    </tr>
                    <tr>
                        <td>ServiceRequest (Category) = referral</td>
                    </tr>
					<tr>
                        <td>ServiceRequest (Category) = referraltopharmacy</td>
                    </tr>
                    <tr>
                        <td>Encounter (Status) = triaged/finished</td>
                    </tr>
                    <tr rowspan=3>
                        <td>
                            <b>All resources to include 'lastUpdated' value, under the meta section,</b>                    
                            <b>which must be a later timestamp, on updates, if the content of a particular resource contains updated info. Otherwise,</b>
                            <b>maintain the timestamp originally sent.</b>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</div>

<p>

Additionally the HTTP request header for the **GET ServiceRequest** would be:

```
NHSD-Target-Identifier = {Receiver Service Identifier}
X-Request-Id = <GUID_107>
X-Correlation-Id = <GUID_108>
NHSD-End-User-Organisation = {FHIR Organisation (Base64 Encoded)}
NHSD-Requesting-Practitioner = {FHIR Practitioner (Base64 Encoded)} 
NHSD-Requesting-Software =  {FHIR Device (Base64 Encoded)}
```

The HTTP response header for the **GET ServiceRequest** would be:

```
X-Request-Id = <GUID_107>
X-Correlation-Id = <GUID_108>
```

the HTTP request header for the **POST $process-message** would be:

```
NHSD-Target-Identifier = {Receiver Service Identifier}
X-Request-Id = <GUID_000003>
X-Correlation-Id = <GUID_000002>
NHSD-End-User-Organisation = {FHIR Organisation (Base64 Encoded)}
NHSD-Requesting-Practitioner = {FHIR Practitioner (Base64 Encoded)} 
NHSD-Requesting-Software =  {FHIR Device (Base64 Encoded)}
```

The HTTP response header for the **POST $process-message** would be:

```
X-Request-Id = <GUID_000003>
X-Correlation-Id = <GUID_000002>
```

### Bundle Processing - detailed

Below is a pseudo code example of how a bundle could be processed based on the above workflow variables:

<details>
    <summary>> <b class="barslink">Logical - Based on a logical step through in a code format</b></summary>

```c#
Receive_Request
{
	initialise_variable "messageType" 
	initialise_variable "MessageReason" 
	initialise_variable "RequestType"
	
	//HTTP_Headers
	{
		if (HttpHeaders is null || HttpHeaders not Guid )
			OperationOutcome.issue.code = "invalid"
			throw exception with "REC_BAD_REQUEST"
			then return with HTTP.ResponseCode 400
		else if (HttpHeaders.RequestId == RequestId.AlreadyReceived)
			OperationOutcome.issue.code = "duplicate"
			throw exception with "REC_CONFLICT"
			then return with HTTP.ResponseCode 409
	}
	//Bundle
	{
		if(Bundle.meta.versionID is null)
			OperationOutcome.issue.code = "invariant"
			throw exception with "REC_BAD_REQUEST"
			then return with HTTP.ResponseCode 422
		else if!(Bundle.meta.versionID in versionID.supported)
			OperationOutcome.issue.code = "not-supported"
			throw exception with "REC_UNPROCESSABLE_ENTITY"
			then return with HTTP.ResponseCode 422
	}
	//Contents;
	{
		switch(MessageHeader.eventCoding)
		{
			case "servicerequest-request":
				if (MessageHeader.reason.code == "new" && ServiceRequest.status == "active")
					{
						switch(ServiceRequest.Category)
						{
							case "Referral":
								if (Careplan.status != "completed")
								{
									RequestType = "unknown"
									OperationOutcome.issue.code = "invariant"//A content validation rule failed
									throw exception with "REC_BAD_REQUEST"
									then return  HTTP.ResponseCode 400
								}
								else if(Encounter.Status.In("triaged","finished"))
									RequestType = "Im Receiving a new Referral"
								else
									RequestType = "unknown"
									OperationOutcome.issue.code = "invariant"//A content validation rule failed
									throw exception with "REC_BAD_REQUEST"
									then return  HTTP.ResponseCode 400
								break;
							default:
								RequestType = "unknown"
								OperationOutcome.issue.code = "invariant"//A content validation rule failed
								throw exception with "REC_BAD_REQUEST"
								then return  HTTP.ResponseCode 400;
						}
					}
				else if (MessageHeader.reason.code == "update")
					{
						switch(ServiceRequest.category)
						{
							case "Referral":
								if(ServiceRequest.status.In("entered-in-error","revoked"))
								{RequestType = "im receiving a cancelled referral"}
								else
								{
									RequestType = "unknown"
									OperationOutcome.issue.code = "invariant"//A content validation rule failed
									throw exception with "REC_BAD_REQUEST"
									then return  HTTP.ResponseCode 400								
								}
								break;
							default:
								RequestType = "unknown"
								OperationOutcome.issue.code = "invariant"//A content validation rule failed
								throw exception with "REC_BAD_REQUEST"
								then return  HTTP.ResponseCode 400;
						}
					}
				else
				{
					RequestType = "unknown"
					OperationOutcome.issue.code = "invariant"//A content validation rule failed
					throw exception with "REC_BAD_REQUEST"
					then return  HTTP.ResponseCode 400}
				break;
			case "servicerequest-response":
				if (MessageHeader.Response is null )
				{
						RequestType = "Invalid servicerequest-response"
						OperationOutcome.issue.code = "invariant"//A content validation rule failed
						throw exception with "REC_BAD_REQUEST"
						then return  HTTP.ResponseCode 400;
				}
				else if ( !Message.Response.identifier.existsLocally())
				{
						RequestType = "none or invalid response ID"
						OperationOutcome.issue.code = "not-found"//A content validation rule failed
						throw exception with "REC_NOT_FOUND"
						then return  HTTP.ResponseCode 404;
				}
				switch (ServiceRequest.Category)
					{
						case "Referral":
							if (ServiceRequest.status == "revoked" && MessageHeader.reason.code == "new")
							{ RequestType = "im receiving a Safeguarding DNA response (noshow)" } 
							else
							{
								RequestType = "unknown"
								OperationOutcome.issue.code = "invariant"//A content validation rule failed
								throw exception with "REC_BAD_REQUEST"
								then return  HTTP.ResponseCode 400;
							}
							break;
						default:
							RequestType = "unknown"
							OperationOutcome.issue.code = "invariant"//A content validation rule failed
							throw exception with "REC_BAD_REQUEST"
							then return  HTTP.ResponseCode 400;
					}
			case "booking-request":
				if (MessageHeader.Reason.code== "new" && Appointment.Status == "booked")
					if(slot.IsFree())
					{RequestType = "Im Receiving a new booking.";}
					else
					{
						OperationOutcome.issue.code = "conflict"
						throw exception with "REC_CONFLICT"
						then return with HTTP.ResponseCode 409
					}
				else if (MessageHeader.Reason.code == "update")
					MessageHeaderIsUpdate = true;
					switch (Appointment.Status)
					{
						case "cancelled":
							RequestType = "Im Receiving a booking cancellation."
							break						
						case "entered-in-error":
							RequestType = "Im Receiving a booking cancellation."
							break
						default:
							OperationOutcome.issue.code = "invariant"//A content validation rule failed
							throw exception with "REC_BAD_REQUEST"
							then return with HTTP.ResponseCode 400;
							break;
					}
				else
				{
					OperationOutcome.issue.code = "invariant"//A content validation rule failed
					throw exception with "REC_BAD_REQUEST"
					then return with HTTP.ResponseCode 400;
				}
				break;
			case "booking-response":
						OperationOutcome.issue.code = "invariant"//A content validation rule failed
						throw exception with 'REC_BAD_REQUEST'
						then return with HTTP.ResponseCode 400
						break;
			default:
				OperationOutcome.issue.code = "invariant"//A content validation rule failed
				throw exception with 'REC_BAD_REQUEST'
				then return with HTTP.ResponseCode 400
				break;
		}
		
	}
    //Submit
	{
		
		if (Message == "update")
		{
			if (currentLocalData.LastUpdated > originaRequest.ReceivedDate)
			{
				OperationOutcome.issue.code = "conflict"
				throw exception with 'REC_CONFLICT'
				then return with HTTP.ResponseCode 409
				break;
			}		
			foreach (Entry in Bundle)
			{
				if (currentLocalData.Item.exists)
				{
					if (currentLocalData.LastUpdated > originaRequest.Received)
					{
						OperationOutcome.issue.code = "conflict"
						throw exception with 'REC_CONFLICT'
						then return with HTTP.ResponseCode 409
						break;
					}
					if(Entry.LastUpdated > currentLocalData.Item.meta.LastUpdated && Entry.fullUrl = currentLocalData.Item.fullUrl)
						currentLocalData.Item = Entry.Item
						Entry.SubmitWith(currentLocalData.Item.meta.LastUpdated == Entry.LastUpdated )
					else
						ignore
				}
				else
					Entry.SubmitWith(currentLocalData.Item.meta.LastUpdated == Entry.LastUpdated )					
			}
			Submit(currentLocalData.Bundle.meta.LastUpdated = Bundle.Meta.LastUpdated)
			return HTTP.ResponseCode 200 'OK'
		}
		else
			{
				foreach(Entry in Bundle)
				{
					Entry.SubmitWith(currentLocalData.Item.meta.LastUpdated == Entry.LastUpdated )
					Submit(currentLocalData.Bundle.meta.LastUpdated = Bundle.Meta.LastUpdated)
					return HTTP.ResponseCode 200 'OK'
				}
			}
	}	
}	

```

</details>
<br>

<hr>

<!--
![BaRS FHIR API end-to-end process](https://raw.githubusercontent.com/NHSDigital/booking-and-referral-media/master/src/images/WorkFlows/WorkflowStatus-1.0.0.png)
-->