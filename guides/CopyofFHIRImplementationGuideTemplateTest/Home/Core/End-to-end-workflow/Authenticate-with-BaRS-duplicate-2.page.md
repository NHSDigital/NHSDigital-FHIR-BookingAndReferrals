## Authenticate with BaRS

The sender must have already [connected with our platform](https://digital.nhs.uk/developer/guides-and-documentation/security-and-authorisation/application-restricted-restful-apis-signed-jwt-authentication) in order to generate an access token to make a request of the BaRS API. The sender generates and signs a JWT and sends this request to the BaRS token endpoint which provides an access token to be used to interact with the BaRS API. 
A receiver will follow the same process to interact with BaRS API when providing feedback to an original sender, for example. The sender and receiver switch roles in the workflow for referral in both the current first-of-type use cases. This is only relevant to some Applications and will be detailed in the specific {{pagelink:Applications , text:application guide.}}

<hr>
<br>