---
topic: infrastructure
---

# Infrastructure

The infrastructure components defined as parts of BaRS are offered for use as a set of centralised services that can support workflows and simplify integration between systems.

There are two elements to this infrastructure:

- **a routing proxy** that enables systems to connect to each other in a scalable way that does not require each side to have pre-configured direct connections
- a set of enabling **discovery services** that allow BaRS clients to "discover" events, tasks and requests that have been made using BaRS compliant systems from a number of contexts

The routing proxy is the main infrastructure component of BaRS and is hosted and maintained on the centralised NHS API Management platform. It is comprised of several components but, from a developer perspective, it can be thought of as a proxy. All requests are routed through it, it brokers the endpoint for a given service (on behalf of a Sender) and delivers the request to the Receiver. It can support both national and regional scale service service discovery tools. The BaRS Proxy supports scalable, dynamic interoperability and lowers the barrier of entry.  This centralised infrastructure handles the burden of establishing endpoints and connectivity; a Sender need only communicate with the BaRS proxy and a Receiver only needs to accept requests from it.

Components of BaRS centralised infrastructure are as follows:

| Component             | Description  |
|-----------------------|--------------|
| BaRS  Proxy API       | Senders direct all requests to this Proxy API for all requests.  |   
| Endpoint   catalogue  | A component that holds service identifiers and their corresponding physical addresses. It is capable of supporting national and local directory of services or even standalone   endpoints configured within a single system. Providers will be able to manag their endpoints via an API. |



                                                                                                                                                                                                                                                                         |

<hr>