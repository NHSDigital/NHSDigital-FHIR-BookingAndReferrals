---
topic: APP2-HowDoesItWork
---

## {{page-title}}

This section describes how the primary operations used in this Application works. This diagram illustrates the workflow and interactions of a referral request and booking process:
<br>

![BaRS FHIR API end-to-end process](https://raw.githubusercontent.com/NHSDigital/booking-and-referral-media/master/src/images/WorkFlows/111OnlineBookingandReferralSimplified-1.0.0.svg)

To support the workflows for this Application of the standard the operations that need to be supported are:

### Make a Referral

Making a referral for this Application follows the {{pagelink:core-standardpattern-1.1.3, text:standard pattern for BaRS operations}}.

The message definition that defines this payload for this Application is: {{link:https://fhir.nhs.uk/MessageDefinition/bars-message-servicerequest-request-referral}}

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

Making a booking for this Application follows the {{pagelink:core-standardpattern-1.1.3, text:standard pattern for BaRS operations}}.

The message definition that defines this payload for this Application is: {{link:https://fhir.nhs.uk/MessageDefinition/bars-message-servicerequest-request-referral}}

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
<br><br>

<!--
![BaRS FHIR API end-to-end process](https://raw.githubusercontent.com/NHSDigital/booking-and-referral-media/master/src/images/WorkFlows/WorkflowStatus-1.0.0.png)
-->

### How bookings and referrals map to services in UEC workflows

#### Background

It is common for healthcare IT systems to present a single API endpoint that is shared between multiple healthcare services - this is particularly common where a system is centrally-hosted and multi-tenanted, or where an organisation has a single IT system that is used to provide multiple healthcare services.

For example, an NHS provider organisation, 'Trumpton Community Hospital', which provides several healthcare services available to urgent emergency care services, including an NHS 111 call centre, an Out of Hours (OOH) GP service, an Urgent Treatment Centre (UTC) and an Emergency Department. The OOH GP service may offer two sub-services on DoS: OOH GP Telephone Consultations, and OOH GP Face to face Consultations. 
  
Each of the above would be represented in the DoS as discrete services.

Some service discovery tools (such as the UEC Directory of Services (DoS)) list services at the granular healthcare service level i.e. for each of the above example healthcare services, the DoS will have one or more service records defined. It is these individual service records that are presented to users when searching the DoS.

When a system making a booking (e.g. NHS 111) requests available slots from a healthcare service, it needs to identify exactly which healthcare service it is targeting. This will allow receiving systems to correctly route requests and filter the responses to be relevant to the specific request.

**A Key concept here is that it is the receiver of appointments that controls what is returned. The system making the booking does NO filtering, just showing all the slots that are returned.**
           
#### Use Healthcare Service ID to filter slot requests to specific healthcare services

A search parameter of the HealthcareService (an intrinsic part of FHIR RESTful search) will be sent.

##### As a sender, include the ID of the healthcare service as a parameter

As a sender, include a search parameter specifying the Service Discovery tool ID of the healthcare service to which the query is directed.

<div class="nhsd-m-emphasis-box">
    <div class="nhsd-a-box nhsd-a-box--border-blue">
        <div class="nhsd-m-emphasis-box__content-box">
            <h1 class="nhsd-t-heading-s nhsd-t-word-break">Example</h1>
            <p class="nhsd-t-body-s nhsd-t-word-break">
If the DoS has returned a service "Village Urgent Treatment Centre (Dos Service ID:124459850)", in order to book an appointment at that service, ensuring only the available slots that are specific to that service are returned, include a Service ID parameter in the Slot request.
            </p>      
        </div>
    </div>
</div>        

<p>

##### As a receiver, use the healthcare service ID to filter the slots returned in your response

As a system receiving bookings and referrals and providing slots, ensure that only the appropriate slots are returned slots in your response, honouring the request.

Filtering is based on the HealthcareService specified in the query (to filter slots provided by that specific service), along with a date/time range and the 'status' of the slot i.e. either 'free' or 'busy'.

<div class="nhsd-m-emphasis-box">
    <div class="nhsd-a-box nhsd-a-box--border-blue">
        <div class="nhsd-m-emphasis-box__content-box">
            <h1 class="nhsd-t-heading-s nhsd-t-word-break">Example</h1>
            <p class="nhsd-t-body-s nhsd-t-word-break">
            
A Receiver runs three healthcare services from the same system:

1. Walk-in Centre
2. OOH GP Service
3. Urgent Treatment Centre

Within the system these services are likely to have separate booking schedules. 

The mapping between the healthcare service and booking schedules must align with the potential request for slots that could be received. 

| Service                 | DoS ID | Linked Schedule |
|-------------------------|------------|-----------------|
| Walk-in Centre          | 124459850 | Schedule 1      |
| Urgent Treatment Centre | 2329483525 | Schedule 2      |
| OOH GP Service          | 0123944122 | Schedule 3      |

Schedules can be shared between healthcare services, and such multiple mappings would look like this:

| Service                 | DoS ID | Linked Schedule |
|-------------------------|------------|-----------------|
| Walk-in Centre          | 124459850 | Schedule 1      |
| Urgent Treatment Centre | 2329483525 | Schedule 1      |
| Urgent Treatment Centre | 2329483525 | Schedule 2      |
| OOH GP Service          | 0123944122 | Schedule 2      |
| OOH GP Service          | 0123944122 | Schedule 3      |

As a receiving system, it is essentially up to healthcare service providers to decide how to filter the slots returned but it is important to consider that a sending system will assume that any returned slot is a valid slot for booking - it is important that the slots returned are genuinely available to the patient within the context of the request received.
            </p>      
        </div>
    </div>
</div>

#### Support for booking only services

Some services that are profiled on the Urgent Care Directory of Services are commissioned as "booking only" services. 
This means that these services will only accept a referral if a booking has also been made for that patient. 

If no appointment is available then a referral should not be made. 

To achieve this, a "service attribute" is configurable against services. This will allow the service to be flagged as "booking only". Therefore if this attribute is present on the service all consumer systems should withhold referrals. <a href="https://developer.nhs.uk/apis/dos-api/ccs_fields_v1.5_service_attribute.html" target="_blank">The DoS API documentation for this can be found here</a>.

##### Workflow

An example workflow showing how this might be implemented is illustrated below:

![Booking only workflow](https://raw.githubusercontent.com/NHSDigital/booking-and-referral-media/master/src/images/WorkFlows/DOS-bookingattribute-workflow-1.0.1.svg)

##### Example xml returned:

When requesting DoS service details with "CheckCapacitySummary" DoS API call, there is a section in the returned message for the additional attributes:

```xml
<ns1:attributes>
  <attribute>
    <dataType>string</dataType>
    <name>requirebooking</name>
    <description>The service only accepts referrals with an accompanying booked appointment.</description>
    <value>true</value>
  </attribute>
</ns1:attributes>
```

This attribute will have three possible states:

* not present
* present and false
* present and true

For the first two cases, it can be assumed that referrals can be made without a booking. Only if the attribute is *present* **and** *true* should a referral be witheld if there has been no booking.

<hr>
