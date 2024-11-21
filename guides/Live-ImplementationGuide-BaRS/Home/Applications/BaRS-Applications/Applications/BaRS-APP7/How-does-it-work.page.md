---
topic: APP7-HowDoesItWork
---

## {{page-title}}

This section describes how the primary operations used in this Application work. This diagram illustrates the workflow and interactions of a booking process:

<br>

<img src="https://raw.githubusercontent.com/NHSDigital/NHSDigital-FHIR-BookingAndReferrals/main/BaRS-images/images/WorkFlows/Booking-APP7-MVP-1.0.0-alpha.svg" width="1000"></img></a>

To support the workflows for this Application of the standard the operations that need to be supported are:

Standard patterns for appointment operations: {{page:Home/Core/1.1.3/Appointment-StandardPattern/Index.page.md}}



### Search for slots

During a referral workflow where booking is required, there are two separate processes that need to be undertaken sequentially. The first is to search for slots and once a slot has been selected, a booking can be made. 

The first part of this process involves the **sender** making a request to the **receiver** for slots that match the search criteria. This is a "searching" request that requires the response body to include a "searchset" bundle resource.

The search parameters are defined <a href="https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_0_0#api-Slots-getSlots" target="_blank">on the BaRS API specification documentation</a>.




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
                        <td>Get Slots</td>
                        <td>GET /GetSlots</td>
                        <td>n/a</td>
                        <td>n/a</td>
                    </tr>                    
                </tbody>
            </table>
        </div>
    </div>
</div>

<p>

Additionally the HTTP request header for the **GET Slots** would be:

```
NHSD-Target-Identifier = {Receiver Service Identifier}
X-Request-Id = <GUID_00001>
X-Correlation-Id = <GUID_00002>
NHSD-End-User-Organisation = {FHIR Organisation (Base64 Encoded)}
NHSD-Requesting-Practitioner = {FHIR Practitioner (Base64 Encoded)} 
NHSD-Requesting-Software =  {FHIR Device (Base64 Encoded)}
```

The HTTP response header for the **GET Slots** would be:

```
X-Request-Id = <GUID_00001>
X-Correlation-Id = <GUID_00002>
```





### Make a booking

Making a booking for this Application follows the {{pagelink:Core-StandardPattern-1.1.5, text:standard pattern for BaRS operations}}.

The message definition that defines this payload for this Application is: [BARS Message Definition - Booking Request](https://simplifier.net/nhsbookingandreferrals/messagedefinition-bars-messagedefinition-booking-request)

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
                        <td rowspan=4>Booking Request (New)</td>
                        <td rowspan=4>POST /$process-message{booking-request}</td>
                        <td rowspan=4>Appointment (booked)</td>
                        <td>MessageHeader (EventCoding) = booking-request</td>
                    </tr>
                    <tr>
                        <td>MessageHeader (ReasonCode) = new</td>
                    </tr>
                    <tr>
                        <td>Appointment (Status) = booked</td>
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
X-Request-Id = <GUID_00003>
X-Correlation-Id = <GUID_00002>
NHSD-End-User-Organisation = {FHIR Organisation (Base64 Encoded)}
NHSD-Requesting-Practitioner = {FHIR Practitioner (Base64 Encoded)} 
NHSD-Requesting-Software =  {FHIR Device (Base64 Encoded)}
```

The HTTP response header would be:

```
X-Request-Id = <GUID_00003>
X-Correlation-Id = <GUID_00002>
```

### Cancel a Booking

This diagram illustrates the workflow and interactions of a booking cancellation process:

<br>

<img src="https://raw.githubusercontent.com/NHSDigital/NHSDigital-FHIR-BookingAndReferrals/main/BaRS-images/images/WorkFlows/BookingCancel-APP7-MVP-1.0.0-alpha.svg" width="1000"></img></a>

To cancel a booking this Application follows the {{pagelink:core-standardpattern-1.1.5, text:standard pattern for BaRS operations}} with an additional step. Before beginning the standard pattern as descbribed on the linked section, it is first necessary to retrieve the latest version of the booking from the **receiver** as it may have changed locally. This is done by performing a "GET Appointment by ID" call to the **receiving** system's corresponding API endpoint (via the BaRS proxy).

The response to this request will be the requested Appointment resource which should be checked for its current status to ensure it does not already have a status of "cancelled". If not, this version of the Appointment should be used when re-submitting the modified resource in the POST bundle as described in the {{pagelink:Core-StandardPattern-1.1.5, text:standard pattern}}.

The message definition that defines this payload for this Application is: [BARS Message Definition - Cancel Booking Request](https://simplifier.net/nhsbookingandreferrals/messagedefinition-barsmessagedefinitionbookingrequestcancelled)


As a general principle, when performing an update type of operation (of which cancellation is a special case), only the focus resource is altered. Any resources that are mandated due to contextual, linking or referential integrity reasons play a supporting role, although any resources that include elements that are being changed are included too. This is always defined within the relevant message definition.

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
                        <td>Get Booking</td>
                        <td>GET /Appointment{id}</td>
                        <td>n/a</td>
                        <td>n/a</td>
                    </tr>
                    <tr>
                        <td rowspan=6>Booking Request (Cancel)</td>
                        <td rowspan=6>POST /$process-message{booking-request}</td>
                        <td rowspan=6>Appointment (cancelled)</td>
                        <td>MessageHeader (EventCoding) = booking-request</td>
                    </tr>
                    <tr>
                        <td>MessageHeader (ReasonCode) = update</td>
                    </tr>
                    <tr>
                        <td>Appointment (Status) = cancelled</td>
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

Additionally the HTTP request header for the **GET Appointment** would be:

```
NHSD-Target-Identifier = {Receiver Service Identifier}
X-Request-Id = <GUID_00004>
X-Correlation-Id = <GUID_00002>
NHSD-End-User-Organisation = {FHIR Organisation (Base64 Encoded)}
NHSD-Requesting-Practitioner = {FHIR Practitioner (Base64 Encoded)} 
NHSD-Requesting-Software =  {FHIR Device (Base64 Encoded)}
```

The HTTP response header for the **GET Appointment** would be:

```
X-Request-Id = <GUID_00004>
X-Correlation-Id = <GUID_00002>
```

the HTTP request header for the **POST $process-message** would be:

```
NHSD-Target-Identifier = {Receiver Service Identifier}
X-Request-Id = <GUID_00006>
X-Correlation-Id = <GUID_00002>
NHSD-End-User-Organisation = {FHIR Organisation (Base64 Encoded)}
NHSD-Requesting-Practitioner = {FHIR Practitioner (Base64 Encoded)} 
NHSD-Requesting-Software =  {FHIR Device (Base64 Encoded)}
```

The HTTP response header for the **POST $process-message** would be:

```
X-Request-Id = <GUID_00006>
X-Correlation-Id = <GUID_00002>
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
			then return with HTTP.ResponseCode 400
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
<br><br>

<hr>
