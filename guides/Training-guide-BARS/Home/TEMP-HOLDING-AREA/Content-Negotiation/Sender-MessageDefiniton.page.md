---
topic: content-negotiation-Sender-MessageDefinition
---

# {{page-title}}

Upon Receiving a searchset bundle containing MessageDefinitions from a Receiver the most appropriate message definition(s) need to be ascertained.
The resource versions, useContexts and message types all need to be evaluated.

The below pseudo code gives an example of how this should be carried out, adhering to the rules defined in the Mechanisms section.

``` c#
MessageDefinition Content_Negotiation_Client_MessageDefinition()
{
	var ClientUseCaseCategory = "A1T1";
	var ClientApplicationVersion = "1.0.3";
	var CoreVersion = "1.1.0";
	var Service = GetDoSid();
	var DesiredMessagetype = "https://fhir.nhs.uk/MessageDefinition/bars-message-servicerequest-request";
	
	// GET /MessageDefinitions + Query Param
	ResponseMessageDefinitions = GetMessageDefinition(
		NHSD-Target-Identifier = Service,
		context = ClientUseCaseCategory + Service,
		AcceptHeader += CoreVersion;
	);
	
	foreach(MessageDefinition in ResponseMessageDefinitions)
	{
		//MessageDefinition type
		if (MessageDefinition.url != DesiredMessagetype)
		{break;}

		//Versioning
		var compatible = false;
		
		if (MessageDefinition.version == ClientApplicationVersion)
		{
			compatible = true;
		}
		else if(MessageDefinition.version.MajorVersion > ClientApplicationVersion.MajorVersion)
		{
			compatible = false;
			break; //Version is incompatible.
		}
		else
		{
			compatible = true;
		}
		
		// Context
		foreach(Identifier in MessageDefinition.useContext )
		{
			if(Identifier.system == "https://fhir.nhs.uk/CodeSystem/usecase-categories-bars" && Identifier.code == ClientUseCaseCategory)
			{compatible = true;}
			else{compatible = false; break;}

			if(Identifier.system == "https://fhir.nhs.uk/CodeSystem/dos-id" && Identifier.code == Service)
			{compatible = true;}
			else{compatible = false; break;}
		}
		if(compatible)
		{
			AcceptableMessageDefinitions.Add(MessageDefinition);
		}
	}

	SelectedMessageDef= AcceptableMessageDefinitions.OrderByAscending(Version>="1.0.3").Take(1); // first one closest to 1.0.3

	Return SelectedMessageDef
}
```