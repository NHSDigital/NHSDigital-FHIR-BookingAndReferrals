---
topic: core-TIFailureScenarios-1.1.3
---

## Failure Scenarios

When a message is received, the X-Request-ID and X-Correlation-ID header values are stored appropriately. In this example, this occurs ahead of the message being processed but after any access control is applied by means of the other available headers.

If a message fails due to a message with the same header ids having already been processed, the response must be a 409, REC_CONFLICT with an OperationOutcome.issue.code of 'duplicate' as seen below.

![BaRS FHIR API end-to-end process](https://raw.githubusercontent.com/NHSDigital/booking-and-referral-media/master/src/images/TransactionIntegrity/Initial-failure-scenario-1.0.0.svg)

<br>

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
