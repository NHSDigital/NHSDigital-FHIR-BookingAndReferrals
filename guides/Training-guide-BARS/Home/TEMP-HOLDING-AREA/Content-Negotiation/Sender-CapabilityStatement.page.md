---
topic: core-content-negotiation-Sender-Metadata
---
# {{page-title}}
Upon Receiving a CapabilityStatement in response to GET /metadata from the receiver, the sender needs to confirm the Receiver is capable of completing the desired workflow. This means it must contain all the required functions in the mode of server, at a compatible version, supporting the MessageDefinitions defined by the applications. 

The below pseudo code gives an example of how to accomplish this.

``` c#
bool Content_Negotiation_Client_CapabilityStatement()
{
    List RequiredCapabilities = WorkflowCapabilityRequirements;
    var CoreVersion = "1.1.0";
	var Service = GetDoSid();
	var DesiredMessagetype = "https://fhir.nhs.uk/MessageDefinition/bars-message-servicerequest-request";

    // GET /metadata
    ResponseCapabilityStatement = GetMetadata(
       NHSD-Target-Identifier = Service, 
       AcceptHeader += CoreVersion;
    );
    
    bool compatible = false;
    //Versioning
    if (ResponseCapabilityStatement.version == CoreVersion)
    {
        compatible = true;
    }
    else if(ResponseCapabilityStatement.version.MajorVersion > CoreVersion.MajorVersion)
    {
        compatible = false;
        return compatible; //Version is incompatible.
    }
    else
    {
        compatible = true;
    }

    foreach (RequiredCapability in RequiredCapabilities)
    {
        if(!ResponseCapabilityStatement.Capabilities.Contains(RequiredCapability))
        {
            compatible = false;
            return compatible; //not all capabilities supported
        }
        else
        {
            compatible = true;
        }        
    }

    if(!ResponseCapabilityStatement.messaging.supportedMessage.Contains(DesiredMessagetype as receiver))
    {
        compatible = false; //required message definition not supported.
        return compatible;
    }
    else
    {
        compatible = true;
    }

    return compatible;
}


```