---
topic: APP6-HowDoesItWork
---

## {{page-title}}

This section describes how the primary operations used in this application work. The following diagrams illustrate the workflows and interactions of the following use cases :
* CAD to CAD Out of Area referral
* CAD to CAD Call Assist Request
* CAD to CAD Mutual Aid Request

<br>
<a href="https://raw.githubusercontent.com/NHSDigital/NHSDigital-FHIR-BookingAndReferrals/main/BaRS-Images/WorkFlows/CADOutOfArea-1.0.2.svg" target="_blank>">
<img src="https://raw.githubusercontent.com/NHSDigital/NHSDigital-FHIR-BookingAndReferrals/main/BaRS-Images/WorkFlows/CADOutOfArea-1.0.2.svg" width="1200"></img></a>

<br>
<a href="https://raw.githubusercontent.com/NHSDigital/NHSDigital-FHIR-BookingAndReferrals/main/BaRS-Images/WorkFlows/CADCallAssist-1.0.2.svg" target="_blank>">
<img src="https://raw.githubusercontent.com/NHSDigital/NHSDigital-FHIR-BookingAndReferrals/main/BaRS-Images/WorkFlows/CADCallAssist-1.0.2.svg" width="1200"></img></a>

<br>
<a href="https://raw.githubusercontent.com/NHSDigital/NHSDigital-FHIR-BookingAndReferrals/main/BaRS-Images/WorkFlows/CADMutualAid-1.0.2.svg" target="_blank>">
<img src="https://raw.githubusercontent.com/NHSDigital/NHSDigital-FHIR-BookingAndReferrals/main/BaRS-Images/WorkFlows/CADMutualAid-1.0.2.svg" width="1200"></img></a>

### Actors

| Use Case             | Referral Sender     | Referral Recipient |
| -------------------- | ------------------- | ------------------ |
| Out of Area referral | Call Receiving AST  | Home AST           |
| Call Assist Request  | Home AST            | Supporting AST     |
| Mutual Aid Request   | Home AST            | Supporting AST     |

### Out of Area calls

Calls may be re-routed by the BT Emergency Call Service to an Ambulance Service Trust (AST) outside of the geographic area of the incident (the Call Receiving AST) for the following reasons:
- The Home AST has arrangements with out of area ASTs to take their calls when needed
- A third party caller calls about a patient in another area
- Calls where the incident is on the boundary between two ASTs
    
### Call Assist Requests
A Home AST may request support from a Supporting AST when they cannot send a resource to an incident within their geographic boundary of responsibility. The Supporting AST may accept or reject this request.
- If the Supporting AST rejects the request, the Home AST will make alternative arrangements
- If the Supporting AST accepts the request:
    - the Supporting AST is responsible for dispatching an appropriate resource within the time frame specified by the ARP Priority code
    - the Home AST may close the case on their CAD
    
### Mutual Aid Requests

A Home AST may request support from a Supporting AST when they cannot meet all of the resource requirements for an incident within their geographic boundary of responsibility. The Supporting AST may accept or reject this request.
- If the Supporting AST rejects the request, the Home AST will make alternative arrangements
- If the Supporting AST accepts the request:
    - the Supporting AST is responsible for dispatching the requested resource within the time frame specified in the request
    - the Home AST remains responsible for the case and for dispatching the resources not specified in the request
    
Note: The BaRS Referral may be used to support single patient Mutual aid requests. It is not intended to replace processes relating to Mutual Aid Requests to support Major Incidents with multiple patients.
    
</br>

### This details a BaRS CAD to CAD Referral:

### Receive Call
- When a call is re-routed by BT Emergency Services, call details are also sent electronically to the referral Sender via the Enhanced Information Service for Emergency Calls (EISEC) interface.
- For the Call Assist and Mutual aid use cases, the initial call may be received via BT Emergency Services EISEC interface or directly into the CAD e.g. Healthcare Professional (HCP) direct line

### Create Case
- On receipt of this information the referral Sender's CAD creates a case that is subsequently further populated by system end users, the associated telephony system and other interfaced systems e.g. Clinical Decision Support Systems (CDSS) such as NHS Pathways and Advanced Medical Priority Dispatch System (AMPDS).

### Pre Triage Sieve (PTS)
- On answering the call the referral Sender will undertake a Pre Triage Sieve (PTS) question set to facilitate the early identification of patients with a potentially life-threatening emergency, in order that immediate dispatch of an appropriate resource can take place at the earliest possible point in the call cycle. *If a life-threatening emergency is identified by the PTS the referral Sender AST may make a BaRS referral at this point in the call cycle, and all subsequent information will be communicated in BaRS Referral updates (see Sending a BaRS Referral)*

### Reason for Call
- The referral Sender will capture a Reason for Call based on what the patient or their representative tells them. This may also be known as 'What's the Problem' text or the Presenting complaint.

### Nature of Call (NOC)
- The referral Sender will capture a NOC code to facilitate the early identification of patients with a potentially life-threatening emergency. *If a life-threatening emergency is identified by the NOC, the referral Sender AST may make a BaRS referral at this point in the call cycle, and all subsequent information will be communicated in BaRS Referral updates (see Sending a BaRS Referral below)*
    
### Confirm Location
- The referral Sender will record the location of the incident and confirm using Gazetteer services. This is undertaken at the earliest opportunity and may be prior or subsequent to PTS and NOC.

### Record demographics
- The referral Sender will capture the patient's baseline demographics where possible. This may be followed up by a Personal Demographics Service (PDS) search later in the call cycle.

### Complete Triage
- The referral Sender will complete a triage of the patient to determine the acuity of the case. This will typically be undertaken by a call handler on the Computer Aided Dispatch (CAD) system, using an approved Clinical Decision Support System (CDSS), such as NHS Pathways or AMPDS. *This is the point at which the Referral Sender AST will make a BaRS referral for non-life threatening emergencies; all subsequent information captured will be communicated in BaRS Referral updates (see Sending a BaRS Referral below)*

### Sending a BaRS Referral
- The referral Receiver is identified based on nationally agreed polygons that set geographic boundaries of responsibility for each AST. Service discovery will use these polygons to ascertain the ServiceID of the referral Receiver.
- The Service ID is used to query the BaRS Endpoint Catalogue to identify the referral Receiver's CAD system's endpoint details
- The sender will check that the Receiver supports the intended Referral use case before sending.
- The referral Sender will send the BaRS Referral to the referral Receiver, which includes information required by the referral Receiver to continue the patent's clinical care. This will also include the JourneyID created at the patient's first contact.

### Create Case
- The referral Receiver's CAD will create a new case (Encounter) on receipt of the BaRS Referral and populate it with the patient and clinical details provided in the referral

### Acknowledge Receipt
- The referral Receiver will send an acknowledgement back to the referral Sender, when it has successfully processed the payload. If it fails to do this it will send a BaRS error code. See {{pagelink:core-failure_scenarios-1.3.0, text:failure scenarios}} for more detail.

### Status Update (Referral Response)
- The referral Receiver will send a series of status updates back to the referral Sender, to support tracking the progress of the case.

### Continue updates
- If additional or changed information about the case is captured by the referral Sender, subsequent to sending the BaRS Referral, they may send a BaRS Referral Update to ensure that the referral Receiver has the most up to date information.
- If the referral Sender needs to cancel a Referral, for example the patient calls back and says they do not require an ambulance, they need to send a Cancellation.
- On receipt of a Referral Update, the referral Receiver will send an acknowledgement back to the Sending AST on when it has successfully processed the payload. If it fails to do this it will send a BaRS error code. See {{pagelink:core-failure_scenarios-1.3.0, text:failure scenarios}} for more detail.

### Manage Stack
- The referral Receiver will manage the case in accordance with the Ambulance Response Programme (ARP) Priority Level. This may include:
    - Dispatching an appropriate resource within the specified time frame
    - Validating the triage outcome
    - Referring onward to another care setting e.g. Emergency Department
- When the status of a case changes in the referral Receiver's CAD, a BaRS Status Update will be sent to the referral Sender so they are aware of the current case status.

<br>
<br>

To support the workflows for this application of the standard the operations that need to be supported are:

<hr>

## Make a Referral

Making a referral for this application follows the {{pagelink:Core-StandardPattern-1.3.0, text:standard pattern for BaRS operations}}.

The Message Definition that defines this payload for this application is: {{link:MessageDefinition-BARS-MessageDefinition-ServiceRequest-Request-Referral}}
<p>

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
                        <td>ServiceRequest (Category) = a6t1</td>
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
NHSD-Requesting-Practitioner = {FHIR PractitionerRole (Base64 Encoded)} 
NHSD-Requesting-Software =  {FHIR Device (Base64 Encoded)}
```

The HTTP response header would be:

```
X-Request-Id = <GUID_000001>
X-Correlation-Id = <GUID_000002>
```

### Cancel a Referral

To cancel a referral this Application follows the {{pagelink:core-SPCancellation-1.3.0, text:standard pattern for BaRS cancellation}}. 

The Message Definition that defines the payload for this Application is: {{link:messagedefinition-barsmessagedefinitionservicerequestrequestcancelled}}

If the update-to-cancel is taking place as part of a re-referral routine, once the cancellation is complete, the new referral request can be sent. This step in the workflow would follow the same process as 'Make a Referral' detailed above.

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
                        <td>GET /ServiceRequest/{id}</td>
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
                        <td>ServiceRequest (Category) = a6t1</td>
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
NHSD-Requesting-Practitioner = {FHIR PractitionerRole (Base64 Encoded)} 
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
NHSD-Requesting-Practitioner = {FHIR PractitionerRole (Base64 Encoded)} 
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
					switch(ServiceRequest.Category.coding[0].code) //https://fhir.nhs.uk/CodeSystem/message-category-servicerequest
					{
						case "Referral":
							if (Careplan.status != "active" && CarePlan.intent != "plan" && Task.status != "requested")
							{
								RequestType = "unknown"
								OperationOutcome.issue.code = "invariant"//A content validation rule failed
								throw exception with "REC_BAD_REQUEST"
								then return  HTTP.ResponseCode 400
							}
							else if(Encounter.Status.In("triaged","finished","in-progess")&& Encounter.class.code=="EMER")
							{ 
								switch(ServiceRequest.Category.coding[1].code)  //https://fhir.nhs.uk/CodeSystem/usecases-categories-bars
								{
									case "a6t3":
										RequestType = "Im Receiving a new Mutual Aid Request";
									case:"a6t2":
										RequestType = "Im Receiving a new Call Assist Request";
									case:"a6t1":
										RequestType = "Im Receiving a new Out of Area Request";
								}									
							}
							else
							{
								RequestType = "unknown"
								OperationOutcome.issue.code = "invariant"//A content validation rule failed
								throw exception with "REC_BAD_REQUEST"
								then return  HTTP.ResponseCode 400
							break;
							}
						default:
							RequestType = "unknown"
							OperationOutcome.issue.code = "invariant"//A content validation rule failed
							throw exception with "REC_BAD_REQUEST"
							then return  HTTP.ResponseCode 400;
					}
				}
				else if (MessageHeader.reason.code == "update")
				{
					switch(ServiceRequest.category.coding[0].code) //https://fhir.nhs.uk/CodeSystem/message-category-servicerequest
					{
						case "Referral":
							if(ServiceRequest.status.In("entered-in-error","revoked"))
							{RequestType = "im receiving a cancelled referral"}
							else if (Task.status != "requested")
							{
								RequestType = "unknown"
								OperationOutcome.issue.code = "invariant"//A content validation rule failed
								throw exception with "REC_BAD_REQUEST"
								then return  HTTP.ResponseCode 400
							}
							else if(!LocalServiceRequestData.ResourceId.Contains(ServiceRequest.id))//if ServiceRequest does not exist locally. 
							{
								RequestType = "unknown"
								OperationOutcome.issue.code = "not-found"//A content validation rule failed
								throw exception with "REC_NOT_FOUND"
								then return  HTTP.ResponseCode 400
							}
							else if(Encounter.Status.In("triaged","finished","in-progess")&& Encounter.class.code=="EMER")
							{ 
								switch(ServiceRequest.Category.coding[1].code)  //https://fhir.nhs.uk/CodeSystem/usecases-categories-bars
								{
									case "a6t3":
										RequestType = "Im Receiving a new Mutual Aid Request update";
									case:"a6t2":
										RequestType = "Im Receiving a new Call Assist Request update";
									case:"a6t1":
										RequestType = "Im Receiving a new Out of Area Request update";
								}									
							}
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
					then return  HTTP.ResponseCode 400
					break;
				}
			case "servicerequest-response":
				if (ServiceRequest.status == "active")
					{
						if (MessageHeader.reason.code == "new")
						{
							switch(ServiceRequest.Category.coding[0].code) //https://fhir.nhs.uk/CodeSystem/message-category-servicerequest
							{
								case "Referral":
								if(Encounter.Status.In("planned","finished","in-progess")&& Encounter.class.code=="EMER")
									{ 
										switch(ServiceRequest.Category.coding[1].code)  //https://fhir.nhs.uk/CodeSystem/usecases-categories-bars
										{
											case "a6t3":
												RequestType = "Im Receiving a new Mutual Aid Request response";
											case:"a6t2":
												RequestType = "Im Receiving a new Call Assist Request response";
											case:"a6t1":
												RequestType = "Im Receiving a new Out of Area Request response";
											default:
												RequestType = "unknown"
												OperationOutcome.issue.code = "invariant"//A content validation rule failed
												throw exception with "REC_BAD_REQUEST"
												then return  HTTP.ResponseCode 400;
										}									
									}
								default:
								{
									RequestType = "unknown"
									OperationOutcome.issue.code = "invariant"//A content validation rule failed
									throw exception with "REC_BAD_REQUEST"
									then return  HTTP.ResponseCode 400;
								}
							}	
						}
						else (MessageHeader.reason.code == "update") // Not alpha
						{
							switch(ServiceRequest.Category.coding[0].code) //https://fhir.nhs.uk/CodeSystem/message-category-servicerequest
							{
								case "Referral":
								if(Encounter.Status.In("planned","finished","in-progess")&& Encounter.class.code=="EMER")
									{ 
										switch(ServiceRequest.Category.coding[1].code)  //https://fhir.nhs.uk/CodeSystem/usecases-categories-bars
										{
											case "a6t3":
												RequestType = "Im Receiving a  Mutual Aid Request update response";
											case:"a6t2":
												RequestType = "Im Receiving a  Call Assist Request update response";
											case:"a6t1":
												RequestType = "Im Receiving a  Out of Area Request update response";
											default:
												RequestType = "unknown"
												OperationOutcome.issue.code = "invariant"//A content validation rule failed
												throw exception with "REC_BAD_REQUEST"
												then return  HTTP.ResponseCode 400;
										}									
									}
								default:
								{
									RequestType = "unknown"
									OperationOutcome.issue.code = "invariant"//A content validation rule failed
									throw exception with "REC_BAD_REQUEST"
									then return  HTTP.ResponseCode 400;
								}
							}	
						}
					}
				else if (ServiceRequest.status == "revoked")
				{
					if(Encounter.Status.In("cancelled")&& Encounter.class.code=="EMER")
					{ 
						switch(ServiceRequest.Category.coding[1].code)  //https://fhir.nhs.uk/CodeSystem/usecases-categories-bars
						{
							case "a6t3":
								RequestType = "Im Receiving a new Mutual Aid Request rejection";
							case:"a6t2":
								RequestType = "Im Receiving a new Call Assist Request rejection";
							default:
								RequestType = "unknown"
								OperationOutcome.issue.code = "invariant"//A content validation rule failed
								throw exception with "REC_BAD_REQUEST"
								then return  HTTP.ResponseCode 400;
						}	
					}								
				}
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
				else 
				{
					RequestType = "unknown"
					OperationOutcome.issue.code = "invariant"//A content validation rule failed
					throw exception with "REC_BAD_REQUEST"
					then return  HTTP.ResponseCode 400
					break;
				}				
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
					if(Entry.LastUpdated > currentLocalData.Item.meta.LastUpdated)
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