## Receiver

BaRS will utilise TLS-MA (Mutual Authentication) to communicate with receiving endpoints. Receiving endpoints will require a certificate under the NHS Root CA to facilitate TLS-MA.

- The receiver will need to request a certificate under the NHS Root CA
    - There are two different certificate chains for INT and Prod
    - INT Certificate chains can be found here: https://digital.nhs.uk/services/path-to-live-environments/integration-environment#rootca-and-subca-certificates
    - Prod Certificate chains can be found here: https://digital.nhs.uk/services/path-to-live-environments/live-environment

- The receiving endpoint will present the certificate obtained for TLS-MA
- The receiving endpoint will need to trust the Root CAs and SubCAs for their respective environments
- The receiving endpoint will only accept requests presented with certificates from their respective chains

As the certificates are using the NHS Root CA, fully qualified domain name (FQDN) must be an nhs.uk address, this is the case for both INT and Prod

You need to [apply for your domain](https://digital.nhs.uk/services/networking-addressing/apply-for-an-nhs.uk-domain-for-websites-and-web-applications), ensuring that you complete 'Section 5: For website or application records visible on public internet'.

In production there is a naming convention that must be adhered to. In INT the naming convention should be adhered where possible. In the context of BaRS an example will be:

- ==BaRS-< ODSCode >.< OrganisationName >.nhs.uk== , BaRS is always the application name.

Once you have you have your domain registered you can then begin the process to obtain your certificate by generating a certificate request.

Certificate requests will need to be signed for your endpoint. Note that the FQDN is equal to the certificate name (CN) by convention.

At this point you should have a .key and a .csr files. The next step will be to send the .csr file to be signed by the NHS and get the client certificate.

- If your client certificate will be implemented in any PTL environment then you should send the .csr file to [itoc.supportdesk@nhs.net](mailto:itoc.supportdesk@nhs.net) and they will reply with the certificate (.crt file)

- If your client certificate will be implemented in the PROD environment then the .csr file needs to be send to the DIR team at [dir@nhs.net](mailto:dir@nhs.net) and they will take care of issuing the certificate after validating your request with the Live Services Pipeline at  [liveservices.gate@nhs.net](mailto:liveservices.gate@nhs.net)

<br>
<hr>