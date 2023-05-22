<!-- update the resource.id value to pick the payload and resource to display -->
@```
from Bundle
where id = 'bars-documentation-businesslevelguidance'
for entry where resource.id = '<payload-resourceID>'
	select *
	for resource.parameter
	select {
		FHIR_Element: name,
		Cardinality: min.toString() & '..' & max.toString(),
		Element_Values: documentation.split('|').first(),
		Additional_Guidance: documentation.split('|').tail()
	}

```