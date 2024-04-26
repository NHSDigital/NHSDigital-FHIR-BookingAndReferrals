## Interface

### Introduction

The BaRS API will facilitate the DocumentReference Endpoints for BaRS enabled systems. BaRS will forward the requests for DocumentReferences to the NRL API. Acting as a proxy the BaRS API will verify a producer is authorized.


| BaRS Path                      | Maps to NRLF Path                           | Purpose                                   |
|--------------------------------|---------------------------------------------|-------------------------------------------|
| GET /DocumentReference         | NRL Consumer GET /DocumentReference         | Read Pointers (search)                    |
| GET /DocumentReference/[id]    | NRL Producer GET /DocumentReference/[id]    | Read specific pointer (read before write) |
| POST /DocumentReference        | NRL Producer POST /DocumentReference        | Add a pointer                             |
| PUT /DocumentReference/[id]    | NRL Producer PUT /DocumentReference/[id]    | Update pointer                            |
| Delete /DocumentReference/[id] | NRL Producer DELETE /DocumentReference/[id] | Remove/delete pointer.                    |


### Request and Response

This table describes the two endpoints behaviours for the interaction From a BaRS enabled system through to NRLF.

All Endpoints will use the exsiting Access Control Headers and Transaction Integrity Headers.

| Behaviour       | Initiator     | VERB   | API Path                | Parameters                                                                                  | Payload           | Reactor          | Reactor Behaviour                                                                                                                        | Happy Response | Response Definition                                  |
|-----------------|---------------|--------|-------------------------|---------------------------------------------------------------------------------------------|-------------------|------------------|------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------------------|
| Search Pointers | BaRS Sender   | GET    | /DocumentReference      | Query: subject:identifier<br>Query: custodian:identifier<br>Query: next-page-token<br>Query:type | N/A               | BaRS & NRLF      | BaRS: Request forwarded verbatim to NRLF Consumer Endpoint<br>NRLF: NRLF returns Bundle of DocumentReferences matching search critieria. | 200            | Search Bundle Response containing DocumentReferences |
| Get Pointer     | BaRS Receiver | GET    | /DocumentReference/[id] | Path: id                                                                                    | N/A               | BaRS & NRLF      | BaRS: Request forwarded verbatim to NRLF Producer Endpoint<br>NRLF: NRLF returns Bundle of DocumentReference matching path param [id].   | 200            | DocumentReference                                    |
| Add Pointer     | BaRS Receiver | POST   | /DocumentReference      | N/A                                                                                         | DocumentReference | BaRS & NRLF      | BaRS: Request forwarded verbatim to NRLF Producer Endpoint<br>NRLF: returns a DocumentReference                                          | 201            | OperationOutcome/DocumentReference                   |
| Update Pointer  | BaRS Receiver | PUT    | /DocumentReference/[id] | Path: id                                                                                    | DocumentReference | BaRS & NRLF      | BaRS: Request forwarded verbatim to NRLF Producer Endpoint<br>NRLF: NRLF updates the DocumentReference                                   | 200            | OperationOutcome/DocumentReference                   |
| Delete Pointer  | BaRS Receiver | DELETE | /DocumentReference/[id] | Path: id                                                                                    | DocumentReference | BaRS & NRLF      | BaRS: Request forwarded verbatim to NRLF Producer Endpoint <br>NRLF: NRLF removes the DocumentReference.                                 | 200            | OperationOutcome/DocumentReference                   |

### Parameters

| API Path                | Type  | Parameter            | Format                                              | Purpose                                 | Required? |
|-------------------------|-------|----------------------|-----------------------------------------------------|-----------------------------------------|-----------|
| /DocumentReference      | query | subject:identifier   | https://fhir.nhs.uk/Id/nhs-number|4409815415        | Filter by Patient                       | Y         |
| /DocumentReference      | query | custodian:identifier | https://fhir.nhs.uk/Id/ods-organization-code|Y05868 | Filter by custodian (ODS)               | N         |
| /DocumentReference      | query | next-page-token      | -                                                   | retrieve next set of 20 records         | N         |
| /DocumentReference      | query | type                 | http://snomed.info/sct|736253002                    | Filter by Appointment or ServiceRequesr | N         |
| /DocumentReference/[id] | path  | [ id ]               |                                                     | Specific Document Reference Id.         | Y         |

## Payload