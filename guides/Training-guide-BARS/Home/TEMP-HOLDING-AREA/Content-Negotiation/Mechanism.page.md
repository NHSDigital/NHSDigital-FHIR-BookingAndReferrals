---
topic: content-negotiation-mechanism
---

# {{page-title}}

## Identifying Capabilities 

A particular workflow may leverage an API capability that is not always implemented by a receiver. For example GET /ServiceRequest. The GET /metadata response provides the ability to define what is and is not available. For example, the following entry would be present under the rest.resource element, where the mode is defined as "server", confirming the server can handle the requests required.

``` json
{
					"type": "ServiceRequest",
					"interaction": [
						{
							"code": "read"
						},
						{
							"code": "vread"
						},
						{
							"code": "search-type"
						}
					],
					"searchParam": [
						{
							"name": "_id",
							"type": "token",
							"documentation": "Unique identifier for a ServiceRequest"
						},
						{
							"name": "patient:identifier",
							"type": "token",
							"documentation": "NHS Number (system must be https://fhir.nhs.uk/Id/nhs-number)"
						}
					],
					"versioning": "no-version"
				}
```

Another capability described within the CapabilityStatement is the definition of what MessageDefinitions are supported by the receiver, prior to a GET /MessageDefinition request which will define the message definitions themselves. This will be an array under messaging.supportedMessage. This also defines if they are a sender of the defined message type of a receiver. 

```json
	"supportedMessage": [
				{
					"mode": "receiver",
					"definition": "MessageDefinition/bars-message-booking-request"
				},
				{
					"mode": "receiver",
					"definition": "MessageDefinition/bars-message-servicerequest-request-referral"
				}
	]
```

### The receivers responsibility

The receiver at this level only needs to evaluate the Accept Header to ensure there is no major version discrepancy. A 406 response with the appropriate OprationOutcome should be given if this is the case. 

## Identifying MessageDefinitions

A receivers MessageDefinitions will contain several identifiers that will allow a Sender to ascertain whether their use cases workflow can be completed beyond what the CapabilityStatement has already confirmed. The Message Definition will also contain a version for version negotiation. 
Along with the purpose of the MessageDefinitions purpose of defining the construct of the message, Content negotiation can be completed. Example of identifiers are as follows:

* Name or URL in MessageDefinition.url / MessageDefinition.name : https://fhir.nhs.uk/MessageDefinition/bars-message-servicerequest-request
* Use case in  MessageDefinition.useContext.code[]: https://fhir.nhs.uk/CodeSystem/usecases-categories-bars.
* Service in MessageDefinition.useContext.code[]: https://fhir.nhs.uk/CodeSystem/dos-id
* Version in MessageDefinition.version

The Name or URL define the type of message being sent. The Service id is confirmation of the correct Service. The Use Case Category code(s) define the care setting context required to ensure the message is actionable by the service. The Version allows for Version negotiation. All of these items need to be checked. There may be variations of the same message definition for a given service based on these variables.

### useContext

#### use case
The Use-Case-Category is a codeset that defines the use case for the message, this is defined in the Application the use case is within. A Sender using a particular use case will look for its corresponding code for that use case in this identifier. The Senders subsequent message request will also have this code. This code can also be included in the context query parameter for GET /MessageDefinition to assist in filtering, though the CapabilityStatement will confirm if this is the case or not. It should be evaluated in either eventuality.

#### Service

The Service describes if the MessageDefinition is applicable for this service. This is something that should be implied by the query parameter for GET /MessageDefinition, which acts as a filter. This capability is already described here <link this>.

### Version
The same SemVer rules are applied to the MessageDefinition versions. It could be the case that multiple MessageDefinitions are returned and in this scenario a Sender should select the closest version to their own from a Minor Revision and Patch perspective. If a Major version difference is detected then the Sender cannot continue unless another option is available in the response. 

The receiver at this level only needs to evaluate the Accept Header, again, here to ensure there is no major version discrepancy, and also the service Id in the use context to ensure the correct MessageDefinitions are returned. This may already be taken care of in the logic handling the NHSD-Target-Identifier, however as they are contextually different fields, it is emphasized in this section of the guide. A 404 should be given, with an appropriate OperationOutcome if the context is incorrect.