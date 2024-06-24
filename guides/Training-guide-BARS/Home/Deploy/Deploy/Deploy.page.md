---
topic: deploy
---
## {{page-title}}

<div markdown="span" class="alert alert-warning" role="alert"><i class="fa fa-warning"></i><b> Important:</b>
<p>
This page is intended as guidance for all parties involved in deployments of BaRS stable releases (V1.0 and above). For guidance for Beta deployments see the {{pagelink:Home/Applications/BaRS-Pre-releases/BetaDeploymentGuide.page.md, text:Beta Deployment Guide}}.
</p>
</div>

Implementing a solution requires good knowledge of the environment being deployed to, allowing a plan to be established to check all conditions are met for success. This section covers deployment, along with the necessary checks to prove functionality, to fully test end-to-end capable {{pagelink:Home/Build/Testing-and-Environments, text:environments}}. 

When deploying a solution there are many threads to pull together. The developed solution is one part of this but the local environment it is to be deployed into must also be prepared, as well as  confirming workflow and functionality behave as expected. The fundamental steps will include completing {{pagelink:Home/Build/Testing-and-Environments/Onboarding.page.md, text:BaRS Onboarding}}, upgrading solutions, configuration and testing.

The overall aim is take a solution and enable it in an environment (INT or Production) to work with other deployed solutions. 

#### Prerequisites
In almost all {{pagelink:applications, text:BaRS Applications}}, a solution will act as a Sender and Receiver and need to perform all {{pagelink:Home/Build/Testing-and-Environments/Onboarding.page.md, text:onboarding}} steps. 

Onboarding must occur for each environment independently; the process is similar for each but the steps must be replicated. 

#### Configuration
The core steps to complete technical setup in an environment are:-
* complete {{pagelink:Home/Build/Testing-and-Environments/Onboarding.page.md, text:onboarding}} for the desired environment
* install supplier solution in the given Solution Environment (See Testing section)
* perform any configuration steps to enable BaRS (and related workflows) in the solution 
* provide service identifier* to be configured in the Endpoint Catalogue (BaRS related component)

*This may be a local value or relate to a [directory of service](https://digital.nhs.uk/services/directory-of-services-dos)

**NOTE** - The detail of installing and configuring a solution will differ considerably depending on the supplier and provider(s) involved.