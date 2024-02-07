<a name="top"></a>
## How to use this implementation guide

This section provides a generated <a href="#P1">site map</a> of this implementation guide. 


## Intended Audience

This section describes the type of audience that the section or page is targeted at (if any) where none is stated then the page should be seen as a general page for every reader.

|Audience|Description|
|--
|Clinical|Someone who is reviewing the implementation guide from a clinical perspective, including clinical safety, clinical pathway and informatics; as a clinical professional involved in initial implementations or further roll-out approaches|
|Business|Someone who is reviewing the implementation guide from a business process perspective; as a business analyst looking into workflow and the impact on existing business processes|
|Architect|Someone who is reviewing the implementation guide from an architectural perspective; as a solution architect looking into how this implementation will fit in with existing systems and interfaces |
|FHIR |Someone who is reviewing the implementation guide from a standards perspective; as a person with FHIR knowledge involved in reviewing the implementation guide for compliancy with the FHIR standard or alignment with other FHIR implementations|
|Developer|Someone who is reviewing the implementation guide from a development perspective, the developer who will be coding or involved in the building of the API or system|
|Other|Someone looking into the contents of the implementation guide for any other reason, for example as part of their education or a research project. This type of audience is implied and not shown in the table below.|

## Implementation Guide Format and Structure

The table below gives the reader of this implementation guide guidance about the structure of the guide and an indication of the purpose and intended audience of the sections and pages the guide contains. The intended audience is included to illustrate which type of reader the page is primarily aimed at and of course does not exclude other types of readers from reviewing and feeding back to the team producing the implementation guide.   

Note: not all pages described in the table will be present in every implementation guide as the content is dependent on things such as:

- How the information is exchanged (which FHIR Paradigm used RESTful, Messaging, Document etc.)
- Whether Clinical headings are used in the exchange of the information
- Which FHIR assets are used in the information exchange
- The type of information that is being exchanged 

|Page|Subpage(s)|Description and purpose|Usage|Intended Audience|
|--|--|--|--|--|
|Home||This is the starting point for readers and should be the page that is used when a link is provided to the Implementation Guides|Will be present||
|Introduction||This gives a brief overview of the implementation guidance around things such as: uses cases, scope etc. |Will be present||
||How to use this implementation guide|This gives a generated site map of the implementation guide and guidance to help them understand the implementation guide |Will be present ||
||Release notes|Gives the change history and any additional information to help the reader understand the changes to the guide. The latest changes will be added to the top of the page.|Will be present||
||Guide versioning|Details versioning of implementation guides and what the different stages are, links to a separate guide|Will be present||
||Glossary|A glossary of terms and acronyms used, links to a separate guide|Will be present||
|FHIR Assets||A section that has subpages for each of the FHIR assets, not all FHIR assets are used for all implementations|Will be present|Clinical,Business,Architect,FHIR,Developer|
||Profiles|The page will contain the Profiles for this implementation guide|Will be present|Clinical,Business,Architect,FHIR,Developer|
||Extensions|The page will contain the Extensions used by this implementation guide|Will be present|Clinical,Business,Architect,FHIR,Developer|
||CodeSystems|The page will contain the CodeSystems for this implementation guide|Will be present|Clinical,Business,Architect,FHIR,Developer|
||ValueSets|The page will contain ValueSets for this implementation guide|Will be present|Clinical,Business,Architect,FHIR,Developer|
||ConceptMaps|The page will contain the ConceptMaps for this implementation guide|May be present|Clinical,Business,Architect,FHIR,Developer|
||SearchParameters|The page will contain the SearchParameters for this implementation guide|May be present|Business,Architect,FHIR,Developer|
||OperationDefinitions|The page will contain the OperationDefinitions for this implementation guide|May be present|Business,Architect,FHIR,Developer|
||CapabilityStatements|The page will contain the CapabilityStatements for this implementation guide|May be present|Clinical,Business,Architect,FHIR,Developer|
||Message Definition|The page will contain the Message Definitions for this implementation guide|May be present|Clinical,Business,Architect,FHIR,Developer|
||Naming Systems|The page will contain the Naming Systems for this implementation guide|May be present|Clinical,Business,Architect,FHIR,Developer|
||All Assets|This page is a navigation page and lists the FHIR Asset types|Will be present||
|Design||This section details the design of the FHIR implementation/ use case, it will detail such things as the interactions, transport used, how the data is exchanged etc. |Will be present|Clinical,Business,Architect,FHIR,Developer|
||Design overview|An overview of the design approach|Will be present||
||Data Mapping|The mapping of the data to be exchanged to the FHIR assets. This may be a defined national dataset or just an agreed list of data items for a first of type |May be present|Business,FHIR|
||Interactions|This page will contain text and diagrams which describe how the systems/users/device interact with each other|Will be present|Clinical,Business,Architect,FHIR,Developer|
||Clinical headings|This page describes how the information is structured using clinical headings if they are used|May be present|Clinical,Business|
||Clinical heading[X]|This page may repeat once for each bundle type used, The [X] will be replaced with the heading type  or name|May be present|Clinical,Business|
||Transport|This page will detail the transport layer used for this implementation guide|May be present|Business,Architect|
||FHIR document bundle [X]|This page may repeat once for each bundle type used, The [X] will be replaced with the bundle type or name|May be present|Clinical,Business,Architect,FHIR,Developer|
||FHIR document rendering|This page gives guidance and information on how to render the FHIR document if this is the method of exchange|May be present|Clinical,Business,Developer|
||FHIR document replacement and updates|This page gives guidance and information on how to render the FHIR document if this is the method of exchange|May be present|Business,Developer|
||Use of attachments|If attachments are allowed, this page will detail how they are used, and the types allowed|May be present|Business,Developer|
||Acknowledgments and responses|What acknowledgements or responses are used, if any and how and when to use them|May be present|Clinical,Business,Architect,FHIR|
||Events model|If a events model is used this page will detail what it is and how its used|May be present|Clinical,Business,Architect,FHIR|
||Events publishing and receiving requirements|If this implementation is event based this page will detail publishing and receiving requirements||Clinical,Business,Architect,FHIR|
|Build||This section is about how to build a system or API using this implementation guide|Will be present||
||How to construct bundle|This section details how to construct bundles|May be present|Developers|
|| Bundle [X]|This page may repeat multiple times if there are multiple bundles types exchanged and will give guidance to developers on how to construct the bundles. The [X] will be replaced with the bundle type or name|May be present|Developers|
||How to construct message|This section details how to construct messages|May be present|Developers|
||How to construct message[X]|This page may repeat multiple times if there are multiple message types exchanged and will give guidance to developers on how to construct the messages. The [X] will be replaced with the message type or name|May be present|Developers|
||How to construct clinical coded structures|This section gives guidance on how to construct clinical structures in FHIR instances, for example how to represent a patient's allergies|May be present|Developer|
||How to construct [X]|This page may repeat multiple times if there are multiple clinical structure types exchanged and will give guidance to developers on how to construct the structure type. The [X] will be replaced with the clinical structure type or name|May be present|Developers|
||API usage|This page is used to describe how the API is used in a real life environment|May be present|Clinical,Business,Architect,FHIR,Developer|
||Error handling|Describes any error handling that is applicable for the implementation guide|May be present|Clinical,Business,Architect,FHIR,Developer|
||Query types|The query types supported by this implementation guide, only applicable for REST|May be present|Clinical,Business,Architect,FHIR,Developer|
||Operation responses|This page is used to describe the search operations supported by the API and their responses.|May be present|Clinical,Business,Architect,FHIR,Developer|
|Examples||This page gives an overview of the examples section.|Will be present|Clinical,Business,Architect,FHIR,Developer|
||Example [X]|A page which contains a FHIR example structure. This may be just a single FHIR resource or multiple resources for example a Bundle. The example may be in JSON or XML or both depending on the format used by the implementation|Will be present|Clinical,Business,Architect,FHIR,Developer|
|Authentication||This page needs a brief overview of the authentication section|May be present|Architect,Developer|
||Access control|This page describes the access control guidance or requirements|May be present|Architect,Developer|
||Access tokens|This page describes the access tokens guidance / requirements|May be present|Architect,Developer|
||Auditing|This page describes the auditing requirements|May be present|Architect,Developer|
||Security|This page describes the security guidance / requirements|May be present|Architect,Developer|
||Integration with SPINE|This page describes any guidance / requirements about integration with SPINE.|May be present|Architect,Developer|
|Downloads|This page provides link(s) to download artefacts that may be useful to help with developments such as NPM packages for validation|Will be present|Clinical,Business,Architect,FHIR,Developer|
|Help and support|This page gives contact details for help and support|Will be present|Clinical,Business,Architect,FHIR,Developer|


<h2 id="P1">Site Map</h2>

{{index:root}}



