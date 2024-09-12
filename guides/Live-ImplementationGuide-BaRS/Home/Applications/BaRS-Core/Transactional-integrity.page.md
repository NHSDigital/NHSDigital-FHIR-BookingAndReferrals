## {{page-title}}

Transactional integrity is employed to ensure data integrity is maintained between two parties. It helps ensure that the success or failure of a message is known and can be confirmed. 

There are two existing header items for requests currently available to allow BaRS to meet transactional integrity requirements. They are listed below with their intended uses. The [BaRS API specification](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_0_0) contains example values for these entries.

| Header           | Requirement  | Description                                                                                                                                   | Value                      |
|------------------|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------|----------------------------|
| X-Correlation-ID | Required     | A globally unique identifier for the request that can be used to track related transactions across multiple systems.                          | string representing a GUID |
| X-Request-ID     | Required     | A globally unique identifier for the request, used to de-duplicate repeated requests and to trace the request for support purposes if needed. | string representing a GUID |

Transactional integrity is based on guidance in the [FHIR standard](https://www.hl7.org/fhir/http.html#custom). The header items are used as outlined below:

- the sender will generate both IDs at the beginning of a request for a message.
- the receiver will respond to this initial message, echoing back both IDs. The receiving server does not need to generate a new ID.
- any feedback requests from receiver to the initial sender shall use a new X-Request-ID but retain the X-Correlation-ID. This will be as a new message of the same conversation.
- any subsequent updates from the sender to the receiver shall use a X-Request-ID but will retain the original X-Correlation-ID. This will be as a new message of the same conversation.
- any onward referrals of a message will use a new X-Request-ID but retain the X-Correlation-ID
- a receiver of any message will not accept two messages with the same request and X-Correlation-IDs

### Initial Request

The X-Correlation-ID is a conversation ID for this Encounter or Case. In our initial request both IDs are supplied by the original sender. 

![BaRS FHIR API end-to-end process](https://raw.githubusercontent.com/NHSDigital/booking-and-referral-media/master/src/images/TransactionIntegrity/Initial-Request-1.0.0.svg)

### Sending an update

For an update or subsequent message, a new X-Request-ID is generated, therefore allowing the receiver to accept the new message. The X-Correlation-ID remains unchanged to indicate it is part of the same conversation.

![BaRS FHIR API end-to-end process](https://raw.githubusercontent.com/NHSDigital/booking-and-referral-media/master/src/images/TransactionIntegrity/Sending-An-Update-1.0.0.svg)

### Feedback (response) requests

In the event of feedback (a response), for example, a Safeguarding/DNA message; the receiver (becoming the sender effectively) sends a request to the initial sender with a new X-Request-ID and the same X-Correlation-ID as the original request.

![BaRS FHIR API end-to-end process](https://raw.githubusercontent.com/NHSDigital/booking-and-referral-media/master/src/images/TransactionIntegrity/Feedback-Request-1.0.0.svg)

### Retry scenario

Should a request fail for any reason and the sender not receive a response (in any of the above scenarios) the sender is to retry the request, retaining the same X-Request-ID and X-Correlation-ID as the initial attempt. This allows the receiver to identify whether it has already processed this message or not.

![BaRS FHIR API end-to-end process](https://raw.githubusercontent.com/NHSDigital/booking-and-referral-media/master/src/images/TransactionIntegrity/Retry-Scenario-1.0.0.svg)


This satisfies the need to be able to handle transaction integrity, and for the most part auditing/logging. There are two more scenarios that need to be clarified:

- onwards referrals
- sending a booking and referral

The proposal is to retain the X-Correlation-ID for two separate and distinct messages concerning the same encounter or case.

### Onward Referrals 

The X-Correlation-ID is retained in all interactions. This is beneficial for logging and auditing as using the X-Correlation-ID you can see all interactions for this encounter.

![BaRS FHIR API end-to-end process](https://raw.githubusercontent.com/NHSDigital/booking-and-referral-media/master/src/images/TransactionIntegrity/Onward-Referral-1.0.0.svg)

### Definition of a retry



In this context a retry is an attempt to send the same message, without any changes following a failure. This means:

- the Message body is the same
- the X-Request-ID and X-Correlation-ID are unchanged
- no other header items have changed. (with the potential exemption of the Access Token)

### Receiver responsibilities

- return the  X-Request-ID and X-Correlation-ID in responses at ALL times, where possible
- reject any message with no X-Request-ID and X-Correlation-ID, without exception with REC_BAD_REQUEST (400)
- in the event that a duplicate message that has already been correctly processed is received, return a response with REC_CONFLICT (409) and an operationOutcome.issue.code of "duplicate"
- this combination of codes can only be used in a duplicate message scenario

### Sender responsibilities

The frequency of retries and the duration of a retry period depends on the scenario and should not disrupt workflow. Exponential backoff is considered best practice however it is at the discretion of the sender to define how many times a retry is attempted.

- retry in the event X-Request-ID and X-Correlation-ID is not in the response
- retry in the event no OperationOutcome is in the body of the response
- retry when an OperationOutcome from a receiver contains one of the following values and response codes:
    - REC_TIMEOUT (408)
    - REC_TOO_MANY_REQUESTS (429)
    - REC_UNAVAILABLE (503)
-retry when an OperationOutcome from BaRS itself contains one of the following:
    - PROXY_TIMEOUT / TIMEOUT (504 indicating 408 internally)
    - PROXY_TOO_MANY_REQUESTS / TOO_MANY_REQUESTS (500 indicating a 408 internally)
    - PROXY_UNAVAILABLE  / UNAVAILABLE (503)
- retry when an OperationOutcome from the BaRS API contains one of the following:
    - SEND_TOO_MANY_REQUESTS (429)
    - SEND_FORBIDDEN (403), on the assumption the access token issue is resolved
- it is then at the senders discretion as to whether they update other properties of the message accordingly
- do not retry a request again if a response with the following attributes is received, this indicates the message was successfully sent
    - REC_CONFLICT (409)
    - an operationOutcome.issue.code of "duplicate"

Any intermediary network device responding 'on behalf or in lieu' of the API or the receiver is not likely to respond with an OperationalOutcome or the required X-Request-ID and X-Correlation-ID. Any response not having either one of these properties can be safely deemed a communications failure, a temporary interruption to connectivity or could potentially indicate a service outage. Any of these scenarios could, but not always, warrant an retry. This would be at the discretion of the suppliers however these failed interactions should be logged with as much detail as possible. Errors outside of the HTTP standard should also be logged locally with as much detail as possible, for example; Transport-Layer error messages.

### Failure Scenarios

When a message is received, the X-Request-ID and X-Correlation-ID header values are stored appropriately. In this example, this occurs ahead of the message being processed but after any access control is applied by means of the other available headers.

If a message fails due to a message with the same header ids having already been processed, the response must be a 409, REC_CONFLICT with an OperationOutcome.issue.code of 'duplicate' as seen below.

![BaRS FHIR API end-to-end process](https://raw.githubusercontent.com/NHSDigital/booking-and-referral-media/master/src/images/TransactionIntegrity/Initial-failure-scenario-1.0.0.svg)

### 401 Outcome

<json>

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

	      "code": "security",

	      "details": {

	        "coding": [

	          {

	            "system": "https://fhir.nhs.uk/Codesystem/http-error-codes",

	            "code": "REC_UNAUTHORIZED"

	            "display": "401 - REC_UNAUTHORIZED"        

	          }

	        ]

	      },

	      "diagnostics": "Details of the Exact problem"

	    }

	  ]

	}   

</json>

### 409 Outcome

<json>

	        {

	  "resourceType": "OperationOutcome",

	  "id": "4e2e13af-3bc7-4de3-8cc5-ea4f14d45ef8",

	  "meta": {

	    "profile": [

	      "https://fhir.hl7.org.uk/StructureDefinition/UKCore-OperationOutcome"

	    ]

	  },

	  "issue": [

	    {

	      "severity": "error",

	      "code": "duplicate",

	      "details": {

	        "coding": [

	          {

	            "system": "https://fhir.nhs.uk/Codesystem/http-error-codes",

	            "code": "REC_CONFLICT"

	            "display": "409 - REC_CONFLICT"        

	          }

	        ]

	      },

	      "diagnostics": "This message has already been received and processed"

	    }

	  ]

	}    

</json>

In the event of a timeout, a retry attempt is made after a suitable amount of time to ensure the message was received. The same X-Request-ID and X-Correlation-ID must be used. Should a 409 REC_CONFLICT response be received with a OperationOutcome.issue.code of "duplicate", then this can be used as confirmation that the message was received.

![BaRS FHIR API end-to-end process](https://raw.githubusercontent.com/NHSDigital/booking-and-referral-media/master/src/images/TransactionIntegrity/Timeout-Failure-Scenario-1.0.0.svg)


### 408 Outcome

<json>

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

	      "code": "timeout",

	      "details": {

	        "coding": [

	          {

	            "system": "https://fhir.nhs.uk/Codesystem/http-error-codes",

	            "code": "REC_TIMEOUT"

	            "display": "408 - REC_TIMEOUT"        

	          }

	        ]

	      },

	      "diagnostics": "The connection for this request has timed out."

	    }

	  ]

	}

</json>

### 409 Outcome

<json>

	{

	  "resourceType": "OperationOutcome",

	  "id": "4e2e13af-3bc7-4de3-8cc5-ea4f14d45ef8",

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

	            "display": "409 - REC_CONFLICT"        

	          }

	        ]

	      },

	      "diagnostics": "This message has already been received and processed"

	    }

	  ]

	}

</json>

If the processing of a message is not completed prior to the initial retry, the receiver must respond with a 425 REC_TOO_EARLY response, to indicate the initial message is still processing. The receipt is then unconfirmed and the sender can retry after a suitable amount of time until they receive a desired response.

![BaRS FHIR API end-to-end process](https://raw.githubusercontent.com/NHSDigital/booking-and-referral-media/master/src/images/TransactionIntegrity/Initial-failure-scenario-solution-1.0.0.svg)


### 408 Outcome

<json>

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

	      "code": "timeout",

	      "details": {

	        "coding": [

	          {

	            "system": "https://fhir.nhs.uk/Codesystem/http-error-codes",

	            "code": "REC_TIMEOUT"

	            "display": "408 - REC_TIMEOUT"        

	          }

	        ]

	      },

	      "diagnostics": "The connection for this request has timed out."

	    }

	  ]

	}

</json>

### 425 Outcome

<json>

	{

	  "resourceType": "OperationOutcome",

	  "id": "98ae13af-3bc7-8cc5-4ac7-ea4f14d47dc9",

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

	            "code": "REC_TOO_EARLY"

	            "display": "425 - REC_TOO_EARLY"        

	          }

	        ]

	      },

	      "diagnostics": "The Server has not finished processing the previous attempted request."

	    }

	  ]

	}

</json>

### 409 Outcome

<json>

	{

	  "resourceType": "OperationOutcome",

	  "id": "4e2e13af-3bc7-4de3-8cc5-ea4f14d45ef8",

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

	            "display": "409 - REC_CONFLICT"        

	          }

	        ]

	      },

	      "diagnostics": "This message has already been received and processed"

	    }

	  ]

	}

</json>

The scenarios above describe the response where a message is successful. If a message is not successfully processed following a timeout, the receiver should respond with the response that that failure would have generated. In the diagram below the final response inherits its response from the message that has failed after the timeout.

The relevant 4xx or 5xx response is what the sender receives as a response, ensuring the correct reason for a failure is communicated.


![BaRS FHIR API end-to-end process](https://raw.githubusercontent.com/NHSDigital/booking-and-referral-media/master/src/images/TransactionIntegrity/Post-409-FailureScenario-2-1.0.0.svg)


<hr>