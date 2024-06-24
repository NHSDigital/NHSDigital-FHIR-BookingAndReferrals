## Bundle processing POST /$process-message

This section defines unhappy path scenarios for when a receiver processes a message. This includes a reiteration of Transaction Integrity, workflow variable validations and data conflicts.


### HTTP Headers
Below is a simplified example of how how to handle the Transaction Integrity HTTP headers.
**Logic**
``` c#
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
```
**Visual**

  ![BaRS FHIR API end-to-end process](https://raw.githubusercontent.com/NHSDigital/booking-and-referral-media/master/src/images/FailureScenarios/HTTP-Header-logic-1.0.0.svg)


| HTTP Status Code | HTTP Error Code | issue Code | Scenario                                                          |
|------------------|-----------------|------------|-------------------------------------------------------------------|
| 400              | REC_BAD_REQUEST | invalid    | The request headers are not valid.                                |
| 400              | REC_BAD_REQUEST | required   | The request headers are not present.                              |
| 409              | REC_CONFLICT    | duplicate  | The message has been identified as having already been processed. |

**400 OperationOutcome**
```json
{
  "resourceType": "OperationOutcome",
  "id": "531e073a-3295-4e67-ae90-e00bd96a9cdd",
  "meta": {
    "profile": [
      "https://fhir.hl7.org.uk/StructureDefinition/UKCore-OperationOutcome"
    ]
  },
  "issue": [
    {
      "severity": "error",
      "code": "invalid",
      "details": {
        "coding": [
          {
            "system": "https://fhir.nhs.uk/Codesystem/http-error-codes",
            "code": "REC_BAD_REQUEST"
          }
        ]
      },
      "diagnostics": "Transaction Integrity headers were not present"
    }
  ]
}
```

**409 OperationOutcome**
```json
{
  "resourceType": "OperationOutcome",
  "id": "531e073a-3295-4e67-ae90-e00bd96a9cdd",
  "meta": {
    "profile": [
      "https://fhir.hl7.org.uk/StructureDefinition/UKCore-OperationOutcome"
    ]
  },
  "issue": [
    {
      "severity": "error",
      "code": "duplicate",
      "details": {
        "coding": [
          {
            "system": "https://fhir.nhs.uk/Codesystem/http-error-codes",
            "code": "REC_CONFLICT"
          }
        ]
      },
      "diagnostics": "This message has been recognised as having already been successfully processed."
    }
  ]
}
```

### Message workflow variable validations

Many scenarios are covered by this one example, the full pseudo code can be located at the end of this page. 

**logic**
```c#
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
									RequestType = "unknown"
									OperationOutcome.issue.code = "invariant"//A content validation rule failed
									throw exception with "REC_BAD_REQUEST"
									then return  HTTP.ResponseCode 400;
	 						default:
								RequestType = "unknown"
								OperationOutcome.issue.code = "invariant"//A content validation rule failed
								throw exception with "REC_BAD_REQUEST"
								then return  HTTP.ResponseCode 400;
						}
```

**Visual**

  ![BaRS FHIR API end-to-end process](https://raw.githubusercontent.com/NHSDigital/booking-and-referral-media/master/src/images/FailureScenarios/WorkflowVariable-FailureScenarios-1.0.0.svg)

| HTTP Status Code | HTTP Error Code | issue Code | Scenario                                                                            |
|------------------|-----------------|------------|-------------------------------------------------------------------------------------|
| 400              | REC_BAD_REQUEST | invariant  | A combination of workflow variables has lead to a non-standard or unknown workflow. |

**400 OperationOutcome**
```json
{
  "resourceType": "OperationOutcome",
  "id": "531e073a-3295-4e67-ae90-e00bd96a9cdd",
  "meta": {
    "profile": [
      "https://fhir.hl7.org.uk/StructureDefinition/UKCore-OperationOutcome"
    ]
  },
  "issue": [
    {
      "severity": "error",
      "code": "invariant",
      "details": {
        "coding": [
          {
            "system": "https://fhir.nhs.uk/Codesystem/http-error-codes",
            "code": "REC_BAD_REQUEST"
          }
        ]
      },
      "diagnostics": "A content validation rule failed, Validation message requires a Careplan.satus of 'active'"
    }
  ]
}
```

### Data Conflicts

Receiving an update can present complications under certain conditions if data has been updated locally - for example, If you have updated a record locally prior to an update message being received and a conflict is then encountered. 

**Logic**
``` c#
if (Message == "update")
{
	if (currentLocalData.LastUpdated > originaRequest.ReceivedDate)
	{
		OperationOutcome.issue.code = "conflict"
		throw exception with 'REC_CONFLICT'
		then return with HTTP.ResponseCode 409
		break;
	}	
```
**Visual**

  ![BaRS FHIR API end-to-end process](https://raw.githubusercontent.com/NHSDigital/booking-and-referral-media/master/src/images/FailureScenarios/DataConflict-FailureScenarios-1.0.0.svg)



| HTTP Status Code | HTTP Error Code | issue Code | Scenario                                                     |
|------------------|-----------------|------------|--------------------------------------------------------------|
| 409              | REC_CONFLICT    | conflict   | local data updates conflict with the updates in the message. |

**409 OperationOutcome**
```json
{
  "resourceType": "OperationOutcome",
  "id": "531e073a-3295-4e67-ae90-e00bd96a9cdd",
  "meta": {
    "profile": [
      "https://fhir.hl7.org.uk/StructureDefinition/UKCore-OperationOutcome"
    ]
  },
  "issue": [
    {
      "severity": "error",
      "code": "conflict",
      "details": {
        "coding": [
          {
            "system": "https://fhir.nhs.uk/Codesystem/http-error-codes",
            "code": "REC_CONFLICT"
          }
        ]
      },
      "diagnostics": "Information received has been updated locally and may cause loss, or presents a conflict, of data"
    }
  ]
}
```

## Full Pseudo Code example
Below is the Full Pseudo Code example of the details seen in the workflow variables section.


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
	//Submit //rework this
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