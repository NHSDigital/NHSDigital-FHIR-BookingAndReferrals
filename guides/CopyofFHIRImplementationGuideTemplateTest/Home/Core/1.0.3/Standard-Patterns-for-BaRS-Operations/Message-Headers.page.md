---
topic: core-SPMessageHeader-1.0.3
---

# {{page-title}}

## MessageHeader Resource
BaRS payloads (FHIR message bundles) require a **MessageHeader** FHIR resource which provides key information to drive workflow and start interpreting the data contained within. This resource is central to making a request or asynchronous response and **must** be present in all payloads. 

The **MessageHeader** resource contains the following element which **must** be used as outlined: 
* **MessageHeader.source** -  stipulates where the payload originated. The Sender **must**, under **MessageHeader.source.endpoint**, include a valid URI which could be used as a NHSD-Target-Identifier (their reference on the Endpoint Catalogue) for the Receiver to send an asynchronous response.
* **MessageHeader.destination** - designates who the payload is intended for, including reference to an Organisation resource and a valid URI (*MessageHeader.destination.endpoint*) which is the NHSD-Target-Identifier (their reference on the Endpoint Catalogue) the payload is being sent to.
* **MessageHeader.eventCoding** - determines the 'type' of payload, whether booking, referral, request or asynchronousus response. The value **must** be populated from this [CodeSystem](https://simplifier.net/NHSBookingandReferrals/message-events-bars). In referrals, this value, combined with the *ServiceRequest.category* element, allows supports for different styles of referral to support various use-cases. The value **must** be populated from CodeSystems for [specific type](https://simplifier.net/NHSDigital/message-category-servicerequest) and [use-case](https://simplifier.net/nhsbookingandreferrals/usecases-categories-bars).
* **MessageHeader.reason.code** - indicates whether the message is '**new**' or an '**update**' to something the Receiver is already aware of. The value **must** be populated from this [CodeSystem](https://simplifier.net/NHSBookingandReferrals/message-reason-bars).
* **MessageHeader.focus** -  specifies the root resource through which to start interpreting the payload.
* **MessageHeader.definition** - cites the [MessageDefinition](https://simplifier.net/nhsbookingandreferrals/~resources?category=Example&exampletype=MessageDefinition&sortBy=DisplayName) the payload **must** adhere to and **must** be rejected by the Receiver if it fails to do so. Note: payload conformance to MessageDefinitions is not checked as part of FHIR validation.

When a Receiver begins to process the payload, they **must** initially ensure it is for them and they know who it is from:
* check the **MessageHeader.destination** and verify the **MessageHeader.destination.receiver.reference** refers to their Organisation. 
* check the **MessageHeader.destination.endpoint** is the Service ID they are expected to be processing the request on behalf of. 
* Store **MessageHeader.source.endpoint** as NHSD-Target-Identifier to enable an asynchronous response back to the Sender. Not all workflows will require this type of response but this data must be stored for audit purposes.

Certain elements in MessageHeader explicitly drive workflow, check **MessageHeader.eventCoding** to determine whether a booking or referral payload is being sent, and whether this is an initial or update request or an asynchronous response to a pre-existing request. There are various styles of referral too, a request could be made for a simple 'transfer of care' or, currently, something termed a 'validation', where one service requests another to validate the assessment outcome they have reached. The intention of supporting gradation of referral is to provide BaRS the malleability to support further subtlety of referrals for future use cases. Combining the **MessageHeader.eventCoding** with the **ServiceRequest.cateory** provides this functionality and, with the addition of {{pagelink:core-SPUseCaseCategories-1.0.3, text:use-case categories}} (again populated under **ServiceRequest.category**) specific services are pinpointed through every BaRS workflow. 

Once the above checks have been made, the detail of the payload can start to be unpacked and processed. The structure of the payload **must** be checked first to ensure it adheres to the **MessageHeader.definition** it claims to. The  [MessageDefinitions](https://simplifier.net/nhsbookingandreferrals/~resources?category=Example&exampletype=MessageDefinition&sortBy=DisplayName) will principally be defined by BaRS, at a national level (although bespoke definitions can be used through BaRS), and the Receiver is checking to ensure all mandatory FHIR resources are present and meet their assigned cardinality. This is a manual, business logic, check and not something which is supported through standard FHIR validation of the payload (bundle). 
Next, **MessageHeader.focus** is the root resource through which the payload is intended to be understood. In an initial referral request, this will typically be the **ServiceRequest** FHIR resource. This root will link to other resources to build a narrative for the payload, for example, the **ServiceRequest** will link to the **Encounter** which led to the referral being made and the **Careplan** detailing next actions. The Entity Relationship Diagrams (included in each {{pagelink:Home/Applications/BaRS-Applications/Applications, text:Application}}) are used as a visual representation of the FHIR resource links in the payloads.

<br>
<br>


### Asynchronous Response Workflows

For certain {{pagelink:Home/Applications/BaRS-Applications/Applications, text:Applications}}, an initial request by a Sender expects an asynchronous response (as opposed to an HTTP synchronous response (200) message). These responses are defined by the workflow of the Application and may be consistently returned or conditional. When an asynchronous response is initiated, the original Sender and Receiver roles are switched, the Sender becoming the Receiver and vice versa. This allows BaRS to support complex workflows through support for multiple requests (initial and update) and, potentially, multiple asynchronous responses, for example, an initial status update followed by a more detailed final outcome (as defined in {{pagelink:Home/Applications/BaRS-Applications/Applications/BaRS-APP4, text:Application 4}}). 
The asynchronous response should be thought of as merely another payload, adhering to all the same rules as an initial request or update. Similarly, Sender and Receiver roles are intended to be interchangeable in BaRS and, in most BaRS Applications a supplier is expected to build both Sender and Receiver functionality, something which is reflected in the {{pagelink:Home/Assure/Assure, text:assurance process}}, especially {{pagelink:Home/Core, text:BaRS Core}}.

Where the workflow dictates an asynchronous response is to be sent, the Sender (originally the Receiver) **must** populate: 
* **MessageHeader.response.identifier** with the **Bundle.Id** of the original request payload and set the **MessageHeader.response.code** value to 'ok'.
* Additionally, they **must** follow the above guidance on populating the **MessageHeader**. 








