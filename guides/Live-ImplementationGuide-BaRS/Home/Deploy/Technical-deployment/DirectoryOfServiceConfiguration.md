## {{page-title}}

**Note:** <span style="color:red">**Receiver Firewall Amendments**</span> - Requests from the BaRS API Proxy will originate from **INT** on **35.197.254.55** & **35.246.55.143** and **PROD** on **34.89.0.111** & **34.89.69.6**.

If the provider operates within Urgent and Emergency Care (UEC), they are likely to have a UEC Directory of Services (DoS) entry. DoS leads must configure Service Providers who wish to use BaRS in the standard way, as the service dictates, but their DoS ID will also need to exist in the BaRS Endpoint Catalogue.
Steps to configure the provider on the BaRS Endpoint Catalogue:-
- note the Service ID on DoS
- Obtain API endpoint details for the service from the Supplier or Provider
- Email bookingandreferralstandard@nhs.net with both pieces of information from above, stating the environment to be configured (INT or Prod). 
You should include the proposed dates for testing (if known) to allow the urgency of the request to be set

**Note**: - CareConnect configuration must be maintained alongside the BaRS configuration. This is so senders who are not yet BaRS compliant can still work with CareConnect and GP Connect.

<br>
