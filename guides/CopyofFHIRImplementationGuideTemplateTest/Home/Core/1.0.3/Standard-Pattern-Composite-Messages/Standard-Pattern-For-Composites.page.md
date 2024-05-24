---
topic: core-SPComposites-1.0.3
---

## {{page-title}}

The majority of BaRS operations utilise a single standard approach. Since most BaRS operations involve composites of FHIR resources supporting a particular workflow they all utilise a single type of endpoint designed for processing and consuming of composite resources. This is the $process-message endpoint from the FHIR operations framework. The resource being transmitted in the body of the http request is a FHIR "Bundle" resource. This request payload needs to support two purposes, both the transmission of information as well as an indicator to direct the recieving system to how this particular bundle of resources is to be processed and what workflow should be triggered as a result of its consumption.

These core functions are:

* making a referral
* cancelling/amending a referral
* making a booking
* cancelling/amending a booking
* providing a response/feedback communication

At the highest level this pattern follows the following key steps:

* **Sender** GET the message definition for the payload/workflow being attempted
* **Sender** composes the bundle (as defined by the message definition) ready for POST-ing.
* **Sender** does a POST request to the **receiver**s' /$process-message endpoint.
* **Receiver** inspects the request header and the bundle MessageHeader resource for the *core workflow variables* indicating how to process and consume the bundle.
* **Receiver** send http response message back to the **sender**.

Below is a pseudo code example, showing the above process in detail, illustrating how a message could be interpreted using core workflow variables for a message sent to POST /$process-message.

Each Application will have a tailored example of the below pseudo code. 

<details><summary>> <b class="barslink">Click here to show example</b></summary>

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
							case "Validation":
								if (CarePlan.status != "active")
									{							
										RequestType = "unknown";
										OperationOutcome.issue.code = "invariant";//A content validation rule failed
										throw exception with "REC_BAD_REQUEST";
										then return  HTTP.ResponseCode 400;
									}
								else if(Encounter.Status.In("triaged","in-progress")
									{RequestType = "Im Receiving a new Validation Request";}
								else
									{
										RequestType = "unknown";
										OperationOutcome.issue.code = "invariant";//A content validation rule failed
										throw exception with "REC_BAD_REQUEST";
										then return  HTTP.ResponseCode 400;
									}
								break;
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
							case "Validation":
								if(ServiceRequest.status.In("entered-in-error","revoked"))
									{RequestType = "im receiving a cancelled validation request";}
								else if(ServiceRequest.status.In("active","on-hold"))
									{RequestType = "im receiving an update to a validation request";} 
								else
								{
									RequestType = "unknown"
									OperationOutcome.issue.code = "invariant"//A content validation rule failed
									throw exception with "REC_BAD_REQUEST"
									then return  HTTP.ResponseCode 400								
								}
								break;
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
						case "Validation":
							if(!AnyEncounter.Originates.Local && Encount.Count()<=3)
							{
								if (MessageHeader.Reason.code == "new" && ServiceRequest.status == "active" && MessageHeader.FocusEncounter.status=="in-progress")
								{Request Type = "im receiving a Validation Response interim update" }
								else if (MessageHeader.Reason.code.In ("new","update") && ServiceRequest.status == "completed" && MessageHeader.FocusEncounter.status.In("triaged","complete")
								{Request Type = "im receiving a final Validation Response" }
								else
								{
									RequestType = "unknown"
									OperationOutcome.issue.code = "invariant"//A content validation rule failed
									throw exception with "REC_BAD_REQUEST"
									then return  HTTP.ResponseCode 400;
								}
							}
							else if(MessageHeader.FocusEncounter.status = "triaged" && ServiceRequest.status == "revoked" && MessageHeader.Reason.code.In("new","update"))
							{ RequestType = "im receiving  a Rejected validation response" } // a new encounter here is an edge case.
							else
							{
								RequestType = "unknown"
								OperationOutcome.issue.code = "invariant"//A content validation rule failed
								throw exception with "REC_BAD_REQUEST"
								then return  HTTP.ResponseCode 400;
							}
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
						case "booked":
							RequestType = "Im Receiving an update to a booking."
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
