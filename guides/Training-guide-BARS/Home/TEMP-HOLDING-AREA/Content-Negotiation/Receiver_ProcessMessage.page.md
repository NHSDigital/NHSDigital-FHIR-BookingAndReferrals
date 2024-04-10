---
topic: content-negotiation-Receiver-Process-Message
---
# {{page-title}}

Upon Receiving a message, along with the existing validation and checks present within the rest of BaRS Core and the relevant application; the Receiver should check that the use case category is correct in serviceRequest.category.

The below pseudo code gives an example of how this should be carried out.


``` c#
Receive_Request
{
    string requestUseCase;

    //Versioning
    if (ACCEPTHeader.version == CoreVersion)
    {
        compatible = true;
    }
    else if(ACCEPTHeader.version.MajorVersion > CoreVersion.MajorVersion)
    {
        compatible = false;
			OperationOutcome.issue.code = "not-supported";
			throw exception with "REC_NOT_SUPPORTED";
			then return with HTTP.ResponseCode 406;
    }

    //get the use case from the request
    foreach(codeEntry in ServiceRequest.category.coding)
    {
        if (codeEntry.system == "https://fhir.nhs.uk/CodeSystem/usecase-categories-bars")
        {
            requestUseCase = codeEntry.code;
        }
    }
    // check that use case is applicable to the requested service
    if (requestUseCase not in GetServiceUseCases(MessageHeader.destination.endpoint))
    {
        	OperationOutcome.issue.code = "not-supported";
			throw exception with "REC_UNPROCESSABLE_ENTITY";
			then return with HTTP.ResponseCode 422;
    }

}
```