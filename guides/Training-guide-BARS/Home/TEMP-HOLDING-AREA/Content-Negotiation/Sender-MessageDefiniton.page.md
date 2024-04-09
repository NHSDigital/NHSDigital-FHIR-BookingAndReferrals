``` c#
MessageDefinition Version_negotiation_Client_MessageDefinition()
{
	var ClientUseCaseCategory = "A1T1";
	var ClientVersion = "1.0.3";
	var Service = GetDoSid();
	var DesiredMessagetype = "https://fhir.nhs.uk/MessageDefinition/bars-message-servicerequest-request"
	
	// GET /MessageDefinitions + Query Param
	ResponseMessageDefinitions = GetMessageDefinition(
		NHSD-Target-Identifier = Service,
		context = ClientUseCaseCategory + Service
	);
	
	foreach(MessageDefinition in ResponseMessageDefinitions)
	{
		//MessageDefinition type
		if (MessageDefinition.url != DesiredMessagetype)
		{break;}

		//Versioning
		var compatible = false;
		
		if (MessageDefinition.version == ClientVersion)
		{
			compatible = true;
		}
		else if(MessageDefinition.version.MajorVersion > ClientVersion.MajorVersion)
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
			if(system == "https://fhir.nhs.uk/CodeSystem/usecase-categories-bars" && code == ClientUseCaseCategory)
			{compatible = true;}
			else{compatible = false; break;}

			if(system == "https://fhir.nhs.uk/CodeSystem/dos-id" && code == Service)
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