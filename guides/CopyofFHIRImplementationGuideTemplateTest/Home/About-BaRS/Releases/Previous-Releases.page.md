## {{page-title}}

<div class="bars-blg-expander">
<div class="bars-blg-expander-entry" id="v1.4.0">

| Product Link           | Version | Handle  | Phase    | State           | Release Date | Stability  | Change Log Link |
| -----------------------|---------|---------|----------|-----------------|--------------|------------|---------------- |
| Implementation Guide   | 1.4.0   | v1      | Live     | Current Release | 17/01/2024   | Stable     |{{pagelink:trn-General}} |
| {{pagelink:design-core, text:BaRS Core}}              | 1.2.1   | v1      | Live     | Current Release | 23/11/2023   | Stable     |{{pagelink:trn-core, text: BaRS Core Change Log}} |
| [API Specification](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_1_0)    | 1.1.0   | v1      | Live     | Current Release | 01/04/2023   | Stable     |{{pagelink:trn-api}} |
| {{pagelink: build-testing, text: TKW}}  | 1.0.1   | v1      | Live     | Current Release | 01/04/2023   | Stable     |{{pagelink:trn-tkw}} |
| {{pagelink:application1, text:BaRS-APP1}}   | 1.0.3   | v1      | Live     | Current Release | 11/05/2023   | Stable     |{{pagelink:trn-app1,text:BaRS APP1 Change Log}} |
| {{pagelink:application2, text:BaRS-APP2}}   | 1.0.3   | v1      | Live     | Current Release | 11/05/2023   | Stable     |{{pagelink:trn-app2,text:BaRS APP2 Change Log}} |
| {{pagelink:application3, text:BaRS-APP3}}   | 1.0.0   | v1      | Live     | Current Release | 17/01/2024   | Stable |{{pagelink:trn-app3,text:BaRS APP3 Change Log}} |
| {{pagelink:application4, text:BaRS-APP4}}   | 1.0.0   | v1      | Live     | Current Release | 17/01/2024   | Stable |{{pagelink:trn-app4,text:BaRS APP4 Change Log}} |
| {{pagelink:application5, text:BaRS-APP5}}   | 1.0.0-beta.2  | beta      | Live     | Current Release | 23/11/2023   | Pre-Release |{{pagelink:trn-app5,text:BaRS APP5 Change Log}} |
| {{pagelink:application6, text:BaRS-APP6}}   | 1.0.0-alpha  | beta      | Live     | Current Release | 17/01/2024   | Pre-Release |{{pagelink:trn-app6,text:BaRS APP6 Change Log}} |

### Overview of the release

This release marks the first appearance of Application 6. This is to support an Ambulance service use case where cases need to be moved between different services for operational reasons. Application 6 is released as a "preview" release and has the status of alpha.

Also this release of the BaRS marks the conclusion of the beta period for applications 3 and 4 and this application now moves to a stable v1.0.0 release available for wide use and adoption.

There has also been a number of minor bug fixes and corrections across all other applications

A Clinical Safety assessment of the scope of this release has determined that it has not significantly changed the clinical safety profile of the BaRS. No new Hazards have been identified in this release. The latest version of the BaRS Clinical Safety Case and Hazard Log can be downloaded from the <a href="https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/onboarding-support-information" target="_blank">BaRS FHIR API onboarding support information page</a>.

</div>
</div>

<hr>

<br>

<div class="bars-blg-expander">
<div class="bars-blg-expander-entry" id="v1.3.0">

Product Link           | Version | Handle  | Phase    | State           | Release Date | Stability  | Change Log Link
-----------------------|---------|---------|----------|-----------------|--------------|----------------|--------------
Implementation Guide   | 1.3.0   | v1      | Live     | Current Release | 11/09/2023   | Stable     |{{pagelink:trn-General}}
{{pagelink:design-core, text:BaRS Core}}              | 1.2.0   | v1      | Live     | Current Release | 23/11/2023   | Stable     |{{pagelink:trn-core, text: BaRS Core Change Log}}  
[API Specification](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_1_0)    | 1.1.0   | v1      | Live     | Current Release | 01/04/2023   | Stable     |{{pagelink:trn-api}}
{{pagelink: build-testing, text: TKW}}  | 1.0.1   | v1      | Live     | Current Release | 01/04/2023   | Stable     |{{pagelink:trn-tkw}} 
{{pagelink:application1, text:BaRS-APP1}}   | 1.0.2   | v1      | Live     | Current Release | 11/05/2023   | Stable     |{{pagelink:trn-app1,text:BaRS APP1 Change Log}}
{{pagelink:application2, text:BaRS-APP2}}   | 1.0.2   | v1      | Live     | Current Release | 11/05/2023   | Stable     |{{pagelink:trn-app2,text:BaRS APP2 Change Log}}
{{pagelink:application3, text:BaRS-APP3}}   | 1.0.0-beta   | beta      | Live     | Current Release | 23/11/2023   | Stable |{{pagelink:trn-app3,text:BaRS APP3 Change Log}}
{{pagelink:application4, text:BaRS-APP4}}   | 1.0.0-beta   | beta      | Live     | Current Release | 23/11/2023   | Stable |{{pagelink:trn-app4,text:BaRS APP4 Change Log}}
{{pagelink:application5, text:BaRS-APP5}}   | 1.0.0-beta.1  | beta      | Live     | Current Release | 23/11/2023   | Pre-Release |{{pagelink:trn-app5,text:BaRS APP5 Change Log}}




### Overview of the release

This is a minor point release with non-breaking changes. The main highlight of this release is the first publication of documentation for Applications 3 and 4. Both these applications are at 1.0.0-beta and are about to start public beta testing. There has also been a minor change to the Application 5 beta release to incorporate feedback and scope amendments from the development of public beta participants as well as some recent use case policy updates.

There was also a minor reconfiguration of the guidance across all applications to move a number of sections from the application guidance to the Core guidance in a new section "Standard Patterns for BaRS Operations". The applications now reference these sections via links in the appropriate places. The main purpose for this is to reduce significant duplication across the aplicaitons as these particular operations follow a standard set of patterns that are common across all applications of the standard.

Finally, there was a very small update to the Core documentation to reflect three non-breaking changes to core payloads.

A Clinical Safety assessment of the scope of this release has determined that it has not significantly changed the clinical safety profile of the BaRS. No new Hazards have been identified in this release. The latest version of the BaRS Clinical Safety Case and Hazard Log can be downloaded from the <a href="https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/onboarding-support-information" target="_blank">BaRS FHIR API onboarding support information page</a>. 

</div>
</div>

<hr>
<br>

<div class="bars-blg-expander">
<div class="bars-blg-expander-entry" id="v1.2.0">

Product Link           | Version | Handle  | Phase    | State           | Release Date | Stability  | Change Log Link
-----------------------|---------|---------|----------|-----------------|--------------|----------------|---------------
Implementation Guide   | 1.2.0   | v1      | Live     | Current Release | 11/09/2023   | Stable     |{{pagelink:trn-General}}
{{pagelink:design-core, text:BaRS Core}}              | 1.1.0   | v1      | Live     | Current Release | 30/06/2023   | Stable     |{{pagelink:trn-core, text: BaRS Core Change Log}}  
[API Specification](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_1_0)    | 1.1.0   | v1      | Live     | Current Release | 01/04/2023   | Stable     |{{pagelink:trn-api}}
{{pagelink: build-testing, text: TKW}}  | 1.0.0   | v1      | Live     | Current Release | 01/04/2023   | Stable     |{{pagelink:trn-tkw}} 
{{pagelink:application1, text:BaRS-APP1}}   | 1.0.1   | v1      | Live     | Current Release | 11/05/2023   | Stable     |{{pagelink:trn-app1,text:BaRS APP1 Change Log}}
{{pagelink:application2, text:BaRS-APP2}}   | 1.0.1   | v1      | Live     | Current Release | 11/05/2023   | Stable     |{{pagelink:trn-app2,text:BaRS APP2 Change Log}}
{{pagelink:application5, text:BaRS-APP5}}   | 1.0.0-beta   | beta      | Live     | Current Release | 11/09/2023   | pre-release |{{pagelink:trn-app5,text:BaRS APP5 Change Log}}


### Overview of the release

This is a minor release Primarily to update the application supporting Primary Care to Pharmacy referral flows (application 5) from the alpha phase to the beta phase. There have been some very minor updates and fixes mainly to the documentation based on feedback from suppliers and others who have reviewed the alpha release.


A Clinical Safety assessment of the scope of this release has determined that it has not significantly changed the clinical safety profile of the BaRS. No new Hazards have been identified in this release. The latest version of the BaRS Clinical Safety Case and Hazard Log can be downloaded from the <a href="https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/onboarding-support-information" target="_blank">BaRS FHIR API onboarding support information page</a>. 

</div>
</div>

<hr>
<br>

<div class="bars-blg-expander">
<div class="bars-blg-expander-entry" id="v1.1.0">

Product Link           | Version | Handle  | Phase    | State           | Release Date | Stability  | Change Log Link
-----------------------|---------|---------|----------|-----------------|--------------|----------------|------------
Implementation Guide   | 1.1.0   | v1      | Live     | Current Release | 30/06/2023   | Stable     |{{pagelink:trn-General}}
{{pagelink:design-core, text:BaRS Core}}              | 1.1.0   | v1      | Live     | Current Release | 30/06/2023   | Stable     |{{pagelink:trn-core, text: BaRS Core Change Log}}  
[API Specification](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_1_0)    | 1.1.0   | v1      | Live     | Current Release | 01/04/2023   | Stable     |{{pagelink:trn-api}}
{{pagelink: build-testing, text: TKW}}  | 1.0.0   | v1      | Live     | Current Release | 01/04/2023   | Stable     |{{pagelink:trn-tkw}} 
{{pagelink:application1, text:BaRS-APP1}}   | 1.0.1   | v1      | Live     | Current Release | 11/05/2023   | Stable     |{{pagelink:trn-app1,text:BaRS APP1 Change Log}}
{{pagelink:application2, text:BaRS-APP2}}   | 1.0.1   | v1      | Live     | Current Release | 11/05/2023   | Stable     |{{pagelink:trn-app2,text:BaRS APP2 Change Log}}
{{pagelink:application5, text:BaRS-APP5}}   | 1.0.0-alpha   | v1      | beta     | Current Release | 30/06/2023   | pre-release |{{pagelink:trn-app5,text:BaRS APP5 Change Log}}


### Overview of the release

This is a minor release primarily introducing the pre-release guidance for a new Application of the Booking and Referral Standard. This is the first alpha release supporting Primary Care to Pharmacy referral flows.

A Clinical Safety assessment of the scope of this release has determined that it has not significantly changed the clinical safety profile of the BaRS. No new Hazards have been identified in this release. The latest version of the BaRS Clinical Safety Case and Hazard Log can be downloaded from the <a href="https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/onboarding-support-information" target="_blank">BaRS FHIR API onboarding support information page</a>. 

</div>
</div>

<hr>
<br>

<div class="bars-blg-expander">
<div class="bars-blg-expander-entry" id="v1.0.1">

<a href="https://simplifier.net/guide/nhsbookingandreferralstandard/Home?version=1.0.1" target="_bank">NHS Booking and Referral Standard 1.0.1</a>

Product Link           | Version | Handle  | Phase    | State           | Release Date | Stability  | Change Log Link
-----------------------|---------|---------|----------|-----------------|--------------|----------------|--------------
Implementation Guide   | 1.0.1   | v1      | Live     | Current Release | 11/05/2023   | Stable     |{{pagelink:trn-General}}
{{pagelink:design-core, text:BaRS Core}}              | 1.0.0   | v1      | Live     | Current Release | 01/04/2023   | Stable     |{{pagelink:trn-core, text: BaRS Core Change Log}}  
[API Specification](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_0_0)    | 1.0.0   | v1      | Live     | Current Release | 01/04/2023   | Stable     |{{pagelink:trn-api}}
{{pagelink: build-testing, text: TKW}}  | 1.0.0   | v1      | Live     | Current Release | 01/04/2023   | Stable     |{{pagelink:trn-tkw}} 
{{pagelink:application1, text:BaRS-APP1}}   | 1.0.1   | v1      | Live     | Current Release | 11/05/2023   | Stable     |{{pagelink:trn-app1,text:BaRS APP1 Change Log}}
{{pagelink:application2, text:BaRS-APP2}}   | 1.0.1   | v1      | Live     | Current Release | 11/05/2023   | Stable     |{{pagelink:trn-app2,text:BaRS APP2 Change Log}}

### Overview of the release

This is a minor "patch" adressing a few small issues with the 1.0.0 release of the implementation guide. 

A Clinical Safety assessment of the scope of this Patch release has determined that it has not changed the clinical safety profile of the BaRS since the previous version. No updates have been made to the Clinical Safety Case Report and Hazard Log for this release.

</div>
</div>

<hr>
<br>

<div class="bars-blg-expander">
<div class="bars-blg-expander-entry" id="v1.0.0">

<a href="https://simplifier.net/guide/nhsbookingandreferralstandard/Home?version=1.0.0" target="_bank">NHS Booking and Referral Standard 1.0.0</a>

Product Link           | Version | Handle  | Phase    | State           | Release Date | Stability  | Change Log Link
-----------------------|---------|---------|----------|-----------------|--------------|----------------|-------------
Implementation Guide   | 1.0.0   | v1      | Live     | Released | 01/04/2023   | Stable     |{{pagelink:trn-General}}
{{pagelink:design-core, text:BaRS Core}}              | 1.0.0   | v1      | Live     | Released | 01/04/2023   | Stable     |{{pagelink:trn-core, text: BaRS Core Change Log}}  
[API Specification](https://digital.nhs.uk/developer/api-catalogue/booking-and-referral-fhir/v1_0_0)    | 1.0.0   | v1      | Live     | Released | 01/04/2023   | Stable     |{{pagelink:trn-api}}
{{pagelink: build-testing, text: TKW}}  | 1.0.0    | v1     | Live     | Released | 01/04/2023   | Stable     |{{pagelink:trn-tkw}} 
{{pagelink:application1, text:BaRS-APP1}}   | 1.0.0   | v1      | Live     | Released | 01/04/2023   | Stable     |{{pagelink:trn-app1,text:BaRS APP1 Change Log}}
{{pagelink:application2, text:BaRS-APP2}}   | 1.0.0   | v1      | Live     | Released | 01/04/2023   | Stable     |{{pagelink:trn-app2,text:BaRS APP2 Change Log}}

### Overview of the release

This release constitutes the first stable release of the booking and referral standard (v1.0.0). This release encapsulates all the learning from the first of type (private and public betas) for the first few Applications of the standard.

</div>
</div>

<hr>
<br>