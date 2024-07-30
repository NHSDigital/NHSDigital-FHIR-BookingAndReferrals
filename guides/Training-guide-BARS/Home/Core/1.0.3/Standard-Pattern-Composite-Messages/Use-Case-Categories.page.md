---
topic: core-SPUseCaseCategories-1.0.3
---

# {{page-title}}

One important factor, when making a request of another service, is ensuring the type (or category) of referral being requested is discrete, and sufficiently granular enough, to avoid overlap with other services. For example, a Pharmacy, may support numerous services such as Blood Pressure, New Medicine Service, Oral Contraception, etc.. The Receiver, during the processing of the referral request, will depend upon referral type (among other key information in the request payload) to direct to an appropriate clinical professional or queue etc., dictating the next workflow steps.

The 'type' of referral is categorised at the service level, rather than organisation or system. This service provider level is where BaRS works to define the use-case, to digitise workflow. For example, within the AST (Ambulance Service Trust) referring to AST Service (CAD to CAD), {{pagelink:Home/Applications/BaRS-Applications/Applications/BaRS-APP6/Index.page.md, text:Application6}}, there are three use-cases defined; Out of Area, Mutual Aid and Call Assist. All of these referral request 'types' will end up within the same AST system but the workflows for them differ. These differences could include whether a request is accepted automatically or not, the timeframes an action must be dealt within and the skillset required to undertake the request. A use-case will only ever fit into one BaRS Application, but a BaRS Application may encompass several use-cases, as is the case with Application6. A list of [use-case categories](https://simplifier.net/nhsbookingandreferrals/usecases-categories-bars) have been defined in a specific BaRS CodeSystem which indicate the supported use-cases, and all BaRS compliant solutions must adopt. 

The use-case category is referenced in the initial negotation phase, when a Sender makes a request for MessageDefinitions, and in the subsequent referral request made to the Receiver. The MessageDefinition(s) returned by the Receiver will contain a use-case category code (from the 'use-case-categories' CodeSystem above) under *MessageDefintion.useContext.code*. The Sender **must** read this field to verify the Receiver supports the use-case workflow they intend to engage with. For example, in Application6, certain AST may not support Mutual Aid or Call Assist, therefore, it would be inappropriate to send a referral request to them for either of these use-cases. The Receiver will be able to make this distinction because the Sender's request will include the use-case category code value, under *ServiceRequest.category* and, if it is something they do not support, they will respond with an error (Operation Outcome). 

The sequence of events occurs as follows: 
* the Sender requests the MessageDefintions (which indicate the use-case categories supported) 
* the Sender reads and only engages in the use-case workflows supported
* the Sender's request includes the use-case category code (the same code they read from the MessageDefinition), under ServiceRequest.category
* the Receiver processes accordingly








