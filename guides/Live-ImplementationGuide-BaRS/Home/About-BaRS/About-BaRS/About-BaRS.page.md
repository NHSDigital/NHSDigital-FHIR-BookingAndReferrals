# {{page-title}}

The NHS Booking and Referral standard (known as BaRS) is a **framework standard** for interoperability.

- BaRS offers a **universal** standard way to **digitise workflows** that support all cross service patient journeys in the NHS
- It is based on [FHIR R4]( https://hl7.org/fhir/R4/) and fully supports [UK Core]( https://simplifier.net/hl7fhirukcorer4)
- It is a set of instructions, rules and guidance on how to use the building blocks of FHIR to **digitise workflows**
- This provides a **framework** for suppliers to build solutions in a way that **guarantees compatibility**

The majority of cross service flows in the NHS can be loosely defined as referrals however, there are many more formal definitions of referrals and BaRS is intended to support all of them and more. The primary goal is to create a framework that suppliers can operate within to share information about a patient, with some sort of directive or request for further care or tasks. This can optionally be supported by an appointment (e.g. the reservation of resource for an event at a specific time/place). 


## Summary of the key features

In order to achieve this, BaRS has adopted the approach of standardising everything that can and should be standardised whilst creating a safe space for solutions to have the necessary flexibility to support all flows whilst maintaining compatibility.

There are three main "layers" that make up the framework within BaRS: 

The **first** is the transport layer (referred to as BaRS Core). This is all the things that define the way two systems "talk" to each other and this layer is absolutely standardised. All systems will implement these things exactly the same way. 

**Second** there is the "workflow" layer. This allows a specific BaRS compliant solution to support a particular patient journey. The *way* a workflow is articulated is standardised and each particular workflow is made up of a combination of underlying standard operations (defined in the "transport layer") in a particular sequence.

**Third** there is the Payload layer. The "payloads" are collections of FHIR resources that make up the set of information that is required for the receiving system to complete or deliver the intended service or task that is being requested.

The workflow and payload elements can be predefined or completely dynamic, enabled by the inbuilt content negotiation mechanism, as required by the needs of each specific use case and the sophistication of the systems implementing compliant solutions.

The documentation for BaRS is separated into three groups (or "products"):

- {{pagelink:design-core-1.0.5}} is the foundation containing all the things *everyone* has to do regardless of what flows BaRS is being used to support

- {{pagelink:Applications}}, *apply* the standard to a specific problem and build on this to support specific use cases

- {{pagelink:prereleases}}, this is the same as above but for applications that are in a *pre-release* state, so not generally available until private/public beta is complete.

<br>

## Foundation Principles

During the design and development of the standard, all key decisions are being tested against a set of foundation principles. These were set out at the beginning as a way to ensure that the vision for BaRS is delivered and all decisions are guided by this vision.

**Low Barrier to Entry**

There is little point for a standard with the ambition and scope of BaRS being so difficult to implement that no one actually does. Therefore all decisions are made with the intention of making it as easy as possible for **all** suppliers to build solutions quickly and easily.

**Any-to-Any Connectivity**

From the beginning it has been very important to ensure that all solutions are easily scalable and it is possible to interoperate with another system without any prior knowledge or pre-configuration inplace. So that all interactions are:

- live and "on-the-fly"
- all information is available in realtime from the source
- there is no prior knowledge required for transmission
- there is no requirement for anything to use "point-to-point" interactions (although this approach is supported when approriate)

**Universality**

The primary vision for BaRS has always been to create one standard way of supporting movement of patients and their information accross services. Therefore all decisions have this idea at their heart. Research has allowed us to model the primary, high level steps as a sequence of discrete uncoupled processes that are the same every time these flows happen. 

Additionally, in order to support all possible variations of these flows, the receiver *must* dictate the "payload". 

Rather than the traditional approach of the sender sending everything they know, for the reciever to have to filter out everything they do not need to know, the reciever gets to state what they need to know to do the thing that is being requested of them. No more, no less.

Finally, all decisions are tested against as many obscure and exotic "what-if" scenarios as possible. The intention is to avoid building a standard that only works in one care setting but not another.

If you have come to this implementation guide directly it might be helpful to read some information about the program that is responsible for developing and maininting this standard, please see here: [Booking and Referral Standard (BaRS)](https://digital.nhs.uk/services/booking-and-referral-standard "Booking and Referral Standard (BaRS)") 


## Combining the elements together

It is common to use a recipe analogy to describe complex concepts. It is also possible to describe the payload entities within the BaRS standard using this analogy. In this analogy the recipe is for a specific cake which corresponds to a BaRS Application conformant solution developed by suppliers to enable the digitisation of a use case specific workflow.

![BaRS FHIR API end-to-end process](https://raw.githubusercontent.com/NHSDigital/NHSDigital-FHIR-BookingAndReferrals/main/BaRS-images/images/General/RecipeAnalogy-1.0.0.svg)

**Profiles**

Profiles are the base **ingredients** for the BaRS and come from two sources.

- **UK Core**
 specifies a set of constraints and/or extensions to specific base FHIR resources to enable consistent information flows across UK borders, to improve health and care outcomes for all citizens
 
- **BaRS**
specifies additional constraints and/or extensions to UK core profiles, that are common for all BaRS Applications

**Cardinalities**

All attributes defined in FHIR have cardinality as part of their definition - a minimum number of required appearances and a maximum number. These numbers specify the number of times the attribute may appear in any instance of the resource type. This equates to the **Quantity** in the recipe analogy. Failure to conform to the cardinality of a FHIR attribute will lead to a FHIR validation failure in the same was as altering the quantities of key ingredients will result in a failed cake. See https://hl7.org/fhir/conformance-rules.html for more details about cardinality in FHIR.

**Necessity**

Necessity is an additional layer of conformance and specifies if the population of an element by the SENDER is required for successful execution of the business process that the BaRS Application is enabling. This relates to optionality of ingredients in a recipe. If you want your cake to be a lemon cake, then you MUST add lemons! See Definition of conformance key words for more information.

**Implementation guidance**

Implementation guidance is provided at several levels in the BaRS, for example, at the FHIR element, resource and bundle levels. It describes how these attributes should be populated to support the business process that is used in each BaRS Application. It corresponds to the **Method**  in the recipe analogy, which also can be at the ingredient level or the recipe level.

**Core Payload definition**

BaRS will have Core Payload Definitions that will relate to all BaRS Applications that are build on that definition, e.g.  Urgent Referral. These correspond to a **Basic Recipe**  in the recipe analogy. A good example would be a vanilla sponge. This recipe can be added to to make a variety of cakes for different occasions (or use cases). For BaRS v1.0.0 core payload definitions are not documented as they require more BaRS use cases to be defined so that the common elements can be identified.

**Application**

A BaRS Application consists of implementation guidance that describes how a supplier builds a BaRS conformant solution for a **specific workflow** using the BaRS toolbox. This corresponds to the **Full recipe** for a specific cake, potentially for a 
specific occasion.

<hr>