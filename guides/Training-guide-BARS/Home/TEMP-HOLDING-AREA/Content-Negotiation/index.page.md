---
topic: content-negotiation
---
# Content Negotiation

## Introduction

Content Negotiation within BaRS leverages multiple variables within the CapabilityStatement and MessageDefinition to ensure that a Sender and a Receiver are Compatible. Though some of this is possible due to the Versioning Negotiation, Content Negotiation further builds on that concept with the capabilities published by the server and the identification of message definitions and use cases therein to ensure a workflow can be completed. 

Information obtained from GET /metadata and GET /MessageDefinition will provide the information required to complete Content Negotiation. Along side this, the version variable in the ACCEPT header is also utilised for version negotiation.

## Core vs Application
Within BaRS Core defines the version negotiation, leveraging the accept header completed using SemVer.

The Applications, also using semver, defines the content negotiation and, though employs a similar version negotiation paradigm, is not the same as Core.

These two things combined ensure a Sender and a Receiver are fully compatible within a given workflow.

