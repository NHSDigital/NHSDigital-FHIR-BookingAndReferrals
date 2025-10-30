---
topic: technical deployment
---
## {{page-title}}

<div markdown="span" class="alert alert-warning" role="alert"><i class="fa fa-warning"></i><b> Important:</b>
<p>
This page is intended as guidance for all parties involved in deployments of BaRS stable releases (V1.0 and above). For guidance for Beta deployments see the {{pagelink:Home/Applications/BaRS-Pre-releases/BetaDeploymentGuide.page.md, text:Beta Deployment Guide}}.
</p>
</div>

This is an abbreviated deployment guide, focused exclusively on the technical steps, to connect and configure healthcare Service Providers utilising BaRS. It is aimed at Suppliers and Service Providers (Project Managers, Business Analysts, Application Delivery Specialists, etc.) connecting their solutions to the BaRS Proxy infrastructure and related components.

* Supplier installs BaRS compliant solution to Sender system environment 
* {{pagelink:connect-as-a-sender, text:Connect Sender}} to BaRS Proxy
* Supplier install BaRS compliant solution to Receiver system environment 
* {{pagelink:Connect-as-a-receiver, text:Connect Receiver}} to BaRS Proxy
* Identify or create Service profile(s) for the Receiving service(s) on the chosen national or proprietary Directory of Service* 
* Provide detail of configured services and systems to BaRS Team to {{pagelink:configure-endpoint-catalogue, text:configure in the Endpoint Catalogue}}
* Test configuration between newly configured systems

\* If a Sender is to receive an asynchronous response from the Receiver, as part of the defined workflow, they will also require a Service profile. This will need configuration in the {{pagelink:configure-endpoint-catalogue, text:Endpoint Catalogue}} too.

NB- These steps apply to connecting and configuring systems to both the Integration (INT) and Production (PROD) environment.

<br>
