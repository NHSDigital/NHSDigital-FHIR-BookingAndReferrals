---
topic: core-ErrorHandling-OpOut-1.1.3
---

### OperationOutcome Example

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

	      "code": "invalid",

	      "details": {

	        "coding": [

	          {

	            "system": "https://fhir.nhs.uk/CodeSystem/http-error-codes",

	            "code": "PROXY_BAD_REQUEST",

	            "display": "400 - PROXY_BAD_REQUEST"

	          }

	        ]

	      },

	      "diagnostics": "BaRS encountered a conflict: <further diagnostics information, error message/error text>"

	    }

	  ]

	}
</json>

<br>
<hr>