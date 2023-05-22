# {{page-title}}

BaRS is made up of a set of documentation and optional infrastructure components

## Documentation 

BaRS documentation is as follows:

| Item                             | Description                                                                                                |
|----------------------------------|------------------------------------------------------------------------------------------------------------|
| [BaRS homepage]( https://digital.nhs.uk/services/booking-and-referral-standard)                 | An overview of the BaRS   programme, the benefits of the standard and status of supplier development       |
| Implementation guide (this site) | You will need to use both the BaRS Core page and the BaRS Applications page specific to your use case. |
| [API specification](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir)               | The specification for integrating   with optional BaRS central infrastructure                                      


 
## Infrastructure

The infrastructure components defined as parts of BaRS are offered for use as a set of centralised services that can support workflows and simplify integration between systems.

There are two elements to this infrastructure:

- **a routing proxy** that enables systems to connect to each other in a scalable way that does not require each side to have pre-configured direct connections
- a set of enabling **discovery services** that allow BaRS clients to "discover" events, tasks and requests that have been made using BaRS compliant systems from a number of contexts

The routing proxy is the main infrastructure component of BaRS and is hosted and maintained on the centralised NHS API Management platform. It is comprised of several components but, from a developer perspective, it can be thought of as a proxy. All requests are routed through it, it brokers the endpoint for a given service (on behalf of a sender) and delivers the request to the receiver. It can support both national and regional scale service implementations, including any type of service discovery tool. This centralised infrastructure speeds up your development and rollout by handling the burden of establishing endpoints and connectivity; a sender need only communicate with the BaRS proxy and a receiver only needs to accept requests from it.

Components of BaRS centralised infrastructure are as follows:

| Component             | Description  |
|-----------------------|--------------|
| BaRS  Proxy API       | Senders direct all requests to this Proxy API for all requests.  |   
| Endpoint   catalogue  | A component that holds service identifiers and their corresponding physical addresses. It is capable of supporting national and local directory of services or even standalone   endpoints configured within a single system. Providers will be able to manag their endpoints via an API. |
| BaRS proxy            | The proxy makes the request to the receiver |    


The following components are in development:

| Component | Description                                                                                                                                                                                                                                                                                                                                                                                                                             |
|-----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Registry  | A store of pointers to bookings   and referrals made through BaRS. Receivers will create and maintain the   status of any pointers for the lifecycle of the events they refer to. It is a   store of current active events and cannot be interrogated for historical   ones. Access to the registry will be controlled by authentication at the   API layer and authorisation to access the data will be delegated to the data   owner. |
| Events    | Closely tied with the registry,   this will notify parties (directly related or interested 3rd parties) of   events occurring on pointers in the registry.                                                                                                                                                                                                                                                                              |

<hr>



