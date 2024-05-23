# {{page-title}}

This page defines the foreseen failure scenarios within the BaRS standard and its implementations. The scenarios are broken down by endpoint and describe which HTTP Status Code, BaRS HTTP Error Code and FHIR issue.code to use for each eventuality. In any case, the diagnostics text should reflect the scenarios given and not necessarily be used verbatim.

The rationale, described in the {{pagelink:core-ErrorHandling-1.1.3}} section is that as much information on the nature of the failure as possible is provided in a standard way.

Each scenario has a Source to state whether it is the Proxy or the Receiver which is generating the error. In scenarios where a SEND prefix is provided, the sender is not adhering to the API specification in one way or another.

Note, in future, the PROXY prefix will no longer be used, and errors from the Proxy will use a code with no prefix.

## General Failure Scenarios
This section will define errors that could be seen in any given step and shared from function to function without context. All interactions will follow these rules as such they may be listed in different sections.



| HTTP Status Code | HTTP Error Code                   | issue.Code      | Scenario                                                                                                                                                                                                                                                                 | Source                 |
|------------------|-----------------------------------|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------|
| 400              | SEND_BAD_REQUEST                  | required        | Content invalid against the specification or a profile. ie a required parameter or header is not provided.                                                                                                                                                               | API                    |
| 400              | REC_BAD_REQUEST                   | value           | a header value or parameter is invalid. (these are defined in each specific scenario)                                                                                                                                                                                    | Receiver               |
| 400              | REC_BAD_REQUEST                   | not-supported   | in FOT for when a function or feature in the standard is not yet supported.                                                                                                                                                                                              | Receiver               |
| 400              | PROXY_BAD_REQUEST                 | structure       | When Base64 decoding of the NHSD-Target-Identifier header fails.                                                                                                                                                                                                         | API                    |
| 400              | PROXY_BAD_REQUEST                 | structure       | The NHSD-Target-Identifier header doesn't adhere to the schema                                                                                                                                                                                                           | API                    |
| 401              | SEND_UNAUTHORIZED                 | login / expired | The sender has not provided a token or it has expired or is otherwise invalid.                                                                                                                                                                                           | API                    |
| 405              | SEND_METHOD_NOT_ALLOWED           | not-supported   | using the wrong http verb. For example GET instead of POST                                                                                                                                                                                                                        | API                    |
| 406              | SEND_NOT_ACCEPTABLE               | processing      | The requested resource is capable of generating only content not acceptable according to the Accept headers sent in the request. Versions in Accept or content.<br><br>Version isnt in FOT and should be ignored in FOT if presented. but post FOT it will be evaluated. | API                    |
|                  | REC_NOT_ACCEPTABLE                | processing      | The requested resource is capable of generating only content not acceptable according to the Accept headers sent in the request. Versions in Accept or content.<br><br>Version isnt in FOT and should be ignored in FOT if presented. but post FOT it will be evaluated. | Receiver               |
| 429              | SEND_TOO_MANY_REQUESTS            | throttled       | when rate limiting is applied.                                                                                                                                                                                                                                           | API                    |
| 409              | REC_TIMEOUT                       | timeout         | Injected when a 504 is generated in the proxy due to a receiver timing out on a response.                                                                                                                                                                                | API Injected           |
| 500              | REC_SERVER_ERROR                  | transient       | An unexpected exception has occurred during processing at the receiver.                                                                                                                                                                                                   | Receiver/ API Injected |
| 500              | PROXY_SERVER_ERROR / SERVER ERROR | transient       | An unexpected exception has occurred during processing internally.                                                                                                                                                                                                        | API                    |
| 501              | REC_NOT_IMPLEMENTED               | not-supported   | The receiver has not yet implemented that endpoint or functionality.                                                                                                                                                                                                     | Receiver               |

## Endpoint Catalogue - Message routing.
Below is a diagram of error locations coupled with scenarios with regards to the routing of messages by the proxy using the Endpoint Catalogue. The below diagram is generic in terms of its not API endpoint specific. Most requests will be subject to the errors that can be encountered during message routing.

{{render:EndpointCatalogue-FailureScenarios.drawio}}

#### SEND at the API
When we use the SEND prefix, it is an issue caught before any internal routing or processing occurs, it usually indicates a problem with the format of the request.

These scenarios can be found in other areas however if more required headers are added for endpoints this may be expanded. 

| HTTP Status Code | HTTP Error Code                         | issue Code | Scenario                                                                                                                                                  | Source |
|------------------|-----------------------------------------|------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|--------|
| 400              | SEND_BAD_REQUEST                        | invalid    | The X-Request-Id or the X-Correlation-Id was not included or the NHSD-Target-Identifier was not included.                                                 | API    |
| 401              | SEND_UNAUTHORIZED                       | security   | The user or system was not able to be authenticated, either the access token was invalid, or not provided.                                                | API    |
| 401              | SEND_UNAUTHORIZED                       | unknown    | No Access token was provided.                                                                                                                             | API    |
| 403              | SEND_FORBIDDEN                          | forbidden  | The access token was provided, but BaRS is not enabled.                                                                                                   | API    |
| 404              | PROXY_NOT_FOUND / NOT_FOUND             | not-found  | Endpoint on the API does not exist. This would be a Proxy or non-prefixed response. there is no SEND code for 404 in the value set.                   | API    |
| 500              | PROXY_SERVER_ERROR / SERVER_ ERROR      | exception  | Unexpected error, would expect this to happen internally so this is likely never going to be needed for a SEND and thus unprefixed or PROXY is used here. | API    |
| 503              | PROXY_UNAVAILABLE / SERVICE_UNAVAILABLE | transient  | unlikely to get a OperationOutcome here.                                                                                                                  | API    |

#### PROXY/NONE within the BaRS proxy

| HTTP Status Code | HTTP Error Code                         | issue Code       | Scenario                                                                                                                                           | Source |
|------------------|-----------------------------------------|------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|--------|
| 400              | PROXY_BAD_REQUEST / BAD_REQUEST         | invalid          | The X-Request-Id or the X-Correlation-Id was not included Or the NHSD-Target-Identifier was not included (depending on the endpoint being called). | API    |
| 400              | PROXY_BAD_REQUEST                       | 400              | when Base64 decoding of the NHSD-Target-Identifier header fails.                                                                                   | API    |
| 400              | PROXY_BAD_REQUEST                       | structure        | The NHSD-Target-Identifier header doesn't adhere to the schema                                                                                     | API    |
| 400              | PROXY_BAD_REQUEST / BAD_REQUEST         | required         | A required item is missing. depending on the request/scenario this may be caught by the SEND details above.                                        | API    |
| 400              | PROXY_BAD_REQUEST / BAD_REQUEST         | structure        | A structural issue in the content such as wrong namespace, unable to parse the content completely - ie the Target identifier is malformed.         | API    |
| 404              | PROXY_NOT_FOUND / NOT_FOUND             | not-found        | The resource requested does not exist. For example; the target endpoint does not exist in the Endpoint Catalogue.                                  | API    |
| 404              | PROXY_NOT_FOUND / NOT_FOUND             | multiple-matches | The Target Identifier found two endpoints, this would be an issue with the management of the Endpoint catalogue.                                   | API    |
| 500              | PROXY_SERVER_ERROR / SERVER_ERROR       | exception        | A sub-service encountered an unhandled exception.                                                                                                  | API    |
| 503              | PROXY_UNAVAILABLE / SERVICE_UNAVAILABLE | transient        | A sub-service was unavailable.                                                                                                                      | API    |

#### REC injected at the proxy
When a failure response is received when attempted to forward but no OperationalOutcome is included for a failure scenario. For example, a Timeout.

| HTTP Status Code | HTTP Error Code         | issue Code | Scenario                                                                                                                                                            | Source                     |
|------------------|-------------------------|------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------|
| 408              | REC_TIMEOUT             | timeout    | The connection to the Receiver timed out.                                                                                                                           | Receiver/ Injected at API  |
| 500              | REC_SERVER_ERROR        | exception  | Generic should a 500 response be received but no operation outcome included.                                                                                        | Receiver / Injected at API |
| 503              | REC_SERVICE_UNAVAILABLE | transient  | The response from the receiver was a 503, with no detail. Also useful if there is a connection failure such as the endpoint not being found, or failing to resolve. | Receiver / Injected at API |

#### REC at the receiver. 
| HTTP Status Code | HTTP Error Code  | issue Code | Scenario                                                     | Source                     |
|------------------|------------------|------------|--------------------------------------------------------------|----------------------------|
| 401              | REC_UNAUTHORIZED | security   | Access Control                                               | Receiver                   |
| 403              | REC_FORBIDDEN    | forbidden  | TLS-MA failure.                                              | Receiver                   |
| 403              | REC_FORBIDDEN    | security   | TLS-MA failure.                                              | Receiver                   |
| 500              | REC_SERVER_ERROR | too costly | The request was deemed to costly to process by the receiver. | Receiver                   |
| 500              | REC_SERVER_ERROR | exception  | unhandled exception.                                         | Receiver / Injected at API |
| 500              | REC_SERVER_ERROR | no-store   | internal data storage issue.                                 | Receiver / Injected at API |

## Check Capabilities GET /metadata
Foreseen failure scenarios are limited for this interaction, in the scope of the receiver. The majority of failures for this stage of workflow is mainly going to be at the sender ascertaining the capabilities of the Receiver and whether they can interact. That would be the purpose of this endpoint though and therefore not considered a failure.

{{render:metadata-FailureScenarios}}

#### REC at the receiver

| HTTP Status Code | HTTP Error Code     | issue Code | Scenario                                                                                                                                                       | Source   |
|------------------|---------------------|------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| 400              | REC_BAD_REQUEST     | invalid    | Although this should be caught at the proxy/API, should a request be received with no X-Request-Id or X-Correlation-Id  this check should be in place.         | Receiver |
| 400              | REC_BAD_REQUEST     | value      | Although this should be caught at the proxy/API, should a request be received with an invalid X-Request-Id or X-Correlation-Id  this check should be in place. | Receiver |
| 401              | REC_UNAUTHORIZED    | security   | Access Control issue.                                                                                                                                          | Receiver |
| 403              | REC_FORBIDDEN       | forbidden  | TLS-MA failure.                                                                                                                                                | Receiver |
| 403              | REC_FORBIDDEN       | security   | TLS-MA failure.                                                                                                                                                | Receiver |
| 500              | SERVER_ERROR        | exception  | an unhandled exception has been encountered.                                                                                                                   | Receiver |
| 503              | SERVICE_UNAVAILABLE | transient  | The service(s) is unavailable but is able to respond as such.                                                                                                  | Receiver |

## GET /Slots
Get /Slots has added complexity compared to previous endpoints in this investigation. With a myriad of available and required parameters there is a potential for many scenarios.

#### Rules
* Schedule:actor:HealthcareService - Must be included.
  * For current use cases this will likely match the id in the NHSD-Target-Identifier header. This may not always be the case in future.
* _include - There is a minimum of the following 3 _includes required for current Applications.
  * Slot:schedule
  * Schedule:actor:Practitioner
  * Schedule:actor:HealthcareService
* start - The start parameter must be used twice, and adds the need for handling problematic requests with its use (too wide a time frame, as an example).
  * Must use the [FHIR instant](https://www.hl7.org/fhir/datatypes.html#primitive) format which includes and offset.
  * Must be UTC
  * Must have a greater than and a less than.
* status - The status parameter must be used.
  * multiple statuses must be comma separated.
  * FOT allows free or busy.

#### Interaction  
  {{render:slot-FailureScenarios}}
  
#### Errors by parameter
**Schedule:actor:HealthcareService**

| HTTP Status Code | HTTP Error Code                     | issue Code        | Scenario                                                                                                    | Source           |
|------------------|-------------------------------------|-------------------|-------------------------------------------------------------------------------------------------------------|------------------|
| 400              | SEND_BAD_REQUEST / REC_BAD_REQUEST? | required          | The parameter value was not included in the request. (This parameter is not currently marked as required. ) | API and Receiver |
| 400              | REC_BAD_REQUEST                     | value / invariant | The parameter value was incorrect or wrong.                                                                 | Receiver         |
| 401              | REC_UNAUTHORIZED                    | forbidden         | The Sending organisation/ software/ practitioner Role does is not allowed to access this information.       | Receiver         |
| 404              | REC_NOT_FOUND                       | not-found         | This service does not exist.                                                                                | Receiver         |
 
**_include**

| HTTP Status Code | HTTP Error Code  | issue Code | Scenario                                                                                                    | Source           |
|------------------|------------------|------------|-------------------------------------------------------------------------------------------------------------|------------------|
| 400              | REC_BAD_REQUEST  | required   | the minimum required includes are not present.                                                              | API and Receiver |
| 401              | REC_UNAUTHORIZED | forbidden  | The Sending organisation/ software/ practitioner Role does is not allowed to access this information. | Receiver         |

**start**

| HTTP Status Code | HTTP Error Code                    | issue Code | Scenario                                                                                              | Source           |
|------------------|------------------------------------|------------|-------------------------------------------------------------------------------------------------------|------------------|
| 400              | SEND_BAD_REQUEST / REC_BAD_REQUEST | required   | Date range was not present.                                                                           | API and Receiver |
| 400              | SEND_BAD_REQUEST / REC_BAD_REQUEST | value      | DateTimes in the requested start time range requested was invalid.                                    | API and Receiver |
| 401              | REC_UNAUTHORIZED                   | forbidden  | The Sending organisation/ software/ practitioner Role does is not allowed to access this information. | Receiver         |
| 422              | REC_UNPROCESSABLE_ENTITY           | too-costly | The start time range requested is too wide.                                                           | Receiver         |


**status**

| HTTP Status Code | HTTP Error Code                    | issue Code | Scenario                           | Source           |
|------------------|------------------------------------|------------|------------------------------------|------------------|
| 400              | SEND_BAD_REQUEST / REC_BAD_REQUEST | required   | status not present.                | API and Receiver |
| 400              | SEND_BAD_REQUEST / REC_BAD_REQUEST | value      | status value requested is invalid. | API and Receiver |

**Common Failures**

| HTTP Status Code | HTTP Error Code         | issue Code | Scenario                                                                                                                                                          | Source                  |
|------------------|-------------------------|------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------|
| 400              | REC_BAD_REQUEST         | invalid    | Although this should be caught at the proxy/api, should a request be received with no X-Request-Id or X-Correlation-Id be received this check should be in place. | Receiver                |
| 400              | REC_BAD_REQUEST         | value      | As above, but the value is not a Guid.                                                                                                                            | Receiver                |
| 401              | REC_UNAUTHORIZED        | security   | Access Control issue.                                                                                                                                             | Receiver                |
| 403              | REC_FORBIDDEN           | forbidden  | TLS-MA failure.                                                                                                                                                   | Receiver                |
| 403              | REC_FORBIDDEN           | security   | TLS-MA failure.                                                                                                                                                   | Receiver                |
| 500              | REC_SERVER_ERROR        | exception  | an unhandled exception has been encountered.                                                                                                                      | Receiver / API Injected |
| 503              | REC_SERVICE_UNAVAILABLE | transient  | The service is unavailable but is able to respond as such.                                                                                                        | Receiver / API Injected |

## GET /MessageDefinition
Message definition includes only one additional parameter and therefore there are less scenarios to cover.

#### Rules
* The context query parameter must be present.
    * For current use cases this will always match the value in the NHSD-Target-Identifier header. This could could not always be the case in future.

#### Interactions
  {{render:MessageDefinition-FailureScenarios}}
  
  
#### Errors by parameter

**context**

| HTTP Status Code | HTTP Error Code  | issue Code | Scenario                                         | Source   | Comment |
|------------------|------------------|------------|--------------------------------------------------|----------|---------|
| 400              | SEND_BAD_REQUEST | required   | no context parameter was given.                  | API      |         |
| 400              | REC_BAD_REQUEST  | required   | no context parameter was given.                  | Receiver |         |
| 400              | REC_BAD_REQUEST  | invalid    | the context parameter value was invalid (format) | Receiver |         |
| 400              | REC_BAD_REQUEST  | value      | the context parameter value was invalid (format) | Receiver |         |
| 404              | REC_NOT_FOUND    | not-found  | the context parameter given returned no results. | Receiver |         |

#### Standard errors
| HTTP Status Code | HTTP Error Code         | issue Code | Scenario                                                                                                                                                                                   | Source                  |
|------------------|-------------------------|------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------|
| 400              | REC_BAD_REQUEST         | invalid    | Although this should be caught at the proxy/API, should a request be received with no X-Request-Id or X-Correlation-Id be received this check should be in place. (BaRS without the Proxy) | Receiver                |
| 400              | REC_BAD_REQUEST         | value      | As above, but the value is not a GUID/UUID.                                                                                                                                                     | Receiver                |
| 401              | REC_UNAUTHORIZED        | security   | Access Control issue.                                                                                                                                                                      | Receiver                |
| 403              | REC_FORBIDDEN           | forbidden  | TLS-MA failure.                                                                                                                                                                            | Receiver                |
| 403              | REC_FORBIDDEN           | security   | TLS-MA failure.                                                                                                                                                                            | Receiver                |
| 500              | REC_SERVER_ERROR        | exception  | an unhandled exception has been encountered.                                                                                                                                               | Receiver / API Injected |
| 503              | REC_SERVICE_UNAVAILABLE | transient  | The service(s) is unavailable but is able to respond as such, otherwise injected.                                                                                                          | Receiver / API Injected |

#### GET /Appointment
Defined failure scenarios for the GET /Appointment Endpoint. There are two ways to call this endpoint. Either with a query parameter, or a path parameter. This section covers both of those methods.

#### Rules

**GET /Appointment**
* query parameter identifier patient.identifier must be included.
* query parameter identifier patient.identifier must be a system:value. example: https://fhir.nhs.uk/Id/nhs-number|4857773456

**GET /Appointment/{id}**
* id in path must be a valid GUID/UUID

#### Interactions
  {{render:Appt-FailureScenarios}}
  
#### Errors by parameter
**path id in GET /Appointment{id}**

| HTTP Status Code | HTTP Error Code  | issue Code | Scenario                                                                                      | Source   |
|------------------|------------------|------------|-----------------------------------------------------------------------------------------------|----------|
| 400              | SEND_BAD_REQUEST | required   | The parameter value was not included in the request.                                          | API      |
| 400              | REC_BAD_REQUEST  | required   | The parameter value was not included in the request.                                          | Receiver |
| 400              | REC_BAD_REQUEST  | value      | The identifier was in the incorrect format.                                                   | Receiver |
| 404              | REC_NOT_FOUND    | not-found  | The resource requested was not found.                                                         | Receiver |

**patient:identifier parameter identifier in GET /Appointment**

| HTTP Status Code | HTTP Error Code  | issue Code | Scenario                                                                                      | Source   |
|------------------|------------------|------------|-----------------------------------------------------------------------------------------------|----------|
| 400              | SEND_BAD_REQUEST | required   | The parameter value was not included in the request.                                          | API      |
| 400              | REC_BAD_REQUEST  | required   | The parameter value was not included in the request.                                          | Receiver |
| 400              | SEND_BAD_REQUEST | value      | the identifier was in the incorrect format.                                                   | API      |
| 400              | REC_BAD_REQUEST  | value      | the identifier was in the incorrect format.                                                   | Receiver |

#### GET /ServiceRequest
Defined failure scenarios for the GET /ServiceRequest Endpoint. Much like GET /Appointment there are two ways to call this endpoint. Either with a query parameter, or a path parameter. This section covers both of those methods.

#### Rules

**GET /ServiceRequest**
* query parameter identifier patient.identifier must be included.
* query parameter identifier patient.identifier must be a system:value. example: https://fhir.nhs.uk/Id/nhs-number|4857773456

**GET /ServiceRequest/{id}**
* id in path must be a valid GUID/UUID

#### Interactions
  {{render:SR-FailureScenarios}}

#### Errors by parameter
**path id in GET /ServiceRequest{id}**

| HTTP Status Code | HTTP Error Code  | issue Code | Scenario                                                                                      | Source   |
|------------------|------------------|------------|-----------------------------------------------------------------------------------------------|----------|
| 400              | SEND_BAD_REQUEST | required   | The parameter value was not included in the request.                                          | API      |
| 400              | REC_BAD_REQUEST  | required   | The parameter value was not included in the request.                                          | Receiver |
| 400              | REC_BAD_REQUEST  | value      | The identifier was in the incorrect format.                                                   | Receiver |
| 404              | REC_NOT_FOUND    | not-found  | The resource requested was not found.                                                         | Receiver |

**patient:identifier parameter identifier in GET /ServiceRequest**

| HTTP Status Code | HTTP Error Code  | issue Code | Scenario                                                                                      | Source   |
|------------------|------------------|------------|-----------------------------------------------------------------------------------------------|----------|
| 400              | SEND_BAD_REQUEST | required   | The parameter value was not included in the request.                                          | API      |
| 400              | REC_BAD_REQUEST  | required   | The parameter value was not included in the request.                                          | Receiver |
| 400              | SEND_BAD_REQUEST | value      | the identifier was in the incorrect format.                                                   | API      |
| 400              | REC_BAD_REQUEST  | value      | the identifier was in the incorrect format.                                                   | Receiver |


## Message processing POST /$process-message

This section defines unhappy path scenarios for when a receiver processes a message. This includes a reiteration of Transaction Integrity, workflow variable validations and data conflicts.


#### HTTP Headers
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

{{render:HTTP-Header-Logic}}

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

#### Message workflow variable validations

Many scenarios are covered by this one example, the full pseudo code is?

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
{{render:WorkflowVariable-FailureScenarios}}

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

#### Data Conflicts

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
{{render:DataConflict-FailureScenarios}}


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
Below is the Full Pseudo Code example seen in the workflow variables section.


<details><summary>Click here to show example</summary>

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
				else if (MessageHeader.reason.code =="delete" && ServiceRequest.status = "entered-in-error")
					{
						switch(ServiceRequest.category)
						{
							case "Validation":
								RequestType = "im receiving a cancelled validation request"
								break;
							case "Referral": //must be update
								RequestType = "im receiving a cancelled referral"
								break;
							default:
								OperationOutcome.issue.code = "invariant"//A content validation rule failed
								RequestType = "unknown"
								throw exception with "REC_BAD_REQUEST"
								then return  HTTP.ResponseCode 400
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
				if (MessageHeader.Response is null || !Message.Response.identifier.existsLocally())
				{
						RequestType = "Invalid servicerequest-response, none or invalid response ID"
						OperationOutcome.issue.code = "invariant"//A content validation rule failed
						throw exception with "REC_BAD_REQUEST"
						then return  HTTP.ResponseCode 400;
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
							if(!Encounter.Exists && Encount.Count()<=3)
							{
								if (MessageHeader.Reason.code == "new" && MessageHeader.FocusEncounter.status=="in-progress")
								{Request Type = "im receiving a Validation Response interim update" }
								else if (MessageHeader.Reason.code.In ("new","update") && ServiceRequest.status == "completed" && MessageHeader.FocusEncounter.status== "triaged")
								{Request Type = "im receiving a final Validation Response" }
								else
								{
									RequestType = "unknown"
									OperationOutcome.issue.code = "invariant"//A content validation rule failed
									throw exception with "REC_BAD_REQUEST"
									then return  HTTP.ResponseCode 400;
								}
							}
							else if(Encounter.status = "triaged" && ServiceRequest.status == "revoked" && MessageHeader.Reason.code.In("new","update"))
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
							then return with HTTP.ResponseCode 424002;
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
				if (appointment.Status == 'noshow')
					{RequestType = 'Im Receiving a Safeguarding DNA Feedback cancellation response.'}
				else
					{
						OperationOutcome.issue.code = "invariant"//A content validation rule failed
						throw exception with 'REC_BAD_REQUEST'
						then return with HTTP.ResponseCode 400
						break;
					}
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