# {{page-title}}

The NHS Booking and Referral standard (BaRS) Implementation Guide is intended as a resource to support product and development teams in their BaRS development journey.  You can find out more about what BaRS is, how it works, who it's for and which system suppliers are already assured or working on their development on the [BaRS NHS Service Catalogue](https://digital.nhs.uk/services/booking-and-referral-standard) pages.
 
This section provides information to help you use the Implementation Guide.


## Combining the elements together

It is common to use a recipe analogy to describe complex concepts. It is also possible to describe the payload entities within the BaRS standard using this analogy. In this analogy the recipe is for a specific cake which corresponds to a BaRS Application conformant solution developed by suppliers to enable the digitisation of a use case specific workflow.

![BaRS FHIR API end-to-end process](https://raw.githubusercontent.com/NHSDigital/NHSDigital-FHIR-BookingAndReferrals/main/BaRS-Images/General/RecipeAnalogy-1.0.0.svg)

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