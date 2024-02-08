### Service Request - Request

{{pagelink:Home/FHIRAssets/AllAssets/AllProfiles/BARSMessageHeader-ServiceRequest-Request.guide.md}}

<div class="nhsd-o-expander-list">
  <div class="nhsd-o-expander-list__expander nhsd-!t-margin-bottom-3">
    <div class="nhsd-m-expander">
      <div class="nhsd-a-box nhsd-a-box--bg-light-grey">  
    
        <details>
          <summary class="nhsd-m-expander__heading-container" aria-label="" >
            <div>
              <span class="nhsd-m-expander__icon nhsd-!t-margin-right-1">
                <span class="nhsd-a-icon nhsd-a-icon--size-xs">
                  <svg xmlns="http://www.w3.org/2000/svg" preserveAspectRatio="xMidYMid meet" focusable="false" viewBox="0 0 16 16"><path d="M12,8l-6.5,7L4,13.5L9.2,8L4,2.5L5.5,1L12,8z"/></svg>
                </span>
              </span>
              <p class="nhsd-m-expander__heading nhsd-t-body">Message Header</p>
            </div>
          </summary>
          <div class="nhsd-m-expander__content-container">
            <span class="nhsd-t-body">

The MessageHeader resource carries information such as the sender and receiver as is a wrapper for the message. The event.system and event.code will match the MessageDefinition corresponding values. The definition element has a direct link to the MessageDefinition that will be used to check validation of the Bundle contents.             

### Application specific guidance for this resource:

@```
from Bundle
where id = 'bars-documentation-businesslevelguidance'
for entry where resource.id = 'servicerequestrequest-messageheader-111_ED'
	select *
	for resource.parameter
	select {
		FHIR_Element: name,
		Cardinality: min.toString() & '..' & max.toString(),
		Element_Values: documentation.split('|').first(),
		Additional_Guidance: documentation.split('|').tail()
	}

```
            </span>
          </div>
        </details>
        <details>
          <summary class="nhsd-m-expander__heading-container" aria-label="" >
            <div>
              <span class="nhsd-m-expander__icon nhsd-!t-margin-right-1">
                <span class="nhsd-a-icon nhsd-a-icon--size-xs">
                  <svg xmlns="http://www.w3.org/2000/svg" preserveAspectRatio="xMidYMid meet" focusable="false" viewBox="0 0 16 16"><path d="M12,8l-6.5,7L4,13.5L9.2,8L4,2.5L5.5,1L12,8z"/></svg>
                </span>
              </span>
              <p class="nhsd-m-expander__heading nhsd-t-body">Service Request</p>
            </div>
          </summary>
          <div class="nhsd-m-expander__content-container">
            <span class="nhsd-t-body">

The MessageHeader resource carries information such as the sender and receiver as is a wrapper for the message. The event.system and event.code will match the MessageDefinition corresponding values. The definition element has a direct link to the MessageDefinition that will be used to check validation of the Bundle contents.             

### Application specific guidance for this resource:

@```
from Bundle
where id = 'bars-documentation-businesslevelguidance'
for entry where resource.id = 'servicerequestrequest-messageheader-111_ED'
	select *
	for resource.parameter
	select {
		FHIR_Element: name,
		Cardinality: min.toString() & '..' & max.toString(),
		Element_Values: documentation.split('|').first(),
		Additional_Guidance: documentation.split('|').tail()
	}

```
<iframe src="https://www.simplifier.net/embed/render?id=nhsbookingandreferralstandard/BARSMessageHeader-servicerequest-request" height="345px" width="100%"></iframe>


            </span>
          </div>
        </details>
                <details>
          <summary class="nhsd-m-expander__heading-container" aria-label="" >
            <div>
              <span class="nhsd-m-expander__icon nhsd-!t-margin-right-1">
                <span class="nhsd-a-icon nhsd-a-icon--size-xs">
                  <svg xmlns="http://www.w3.org/2000/svg" preserveAspectRatio="xMidYMid meet" focusable="false" viewBox="0 0 16 16"><path d="M12,8l-6.5,7L4,13.5L9.2,8L4,2.5L5.5,1L12,8z"/></svg>
                </span>
              </span>
              <p class="nhsd-m-expander__heading nhsd-t-body">Healthcare Service</p>
            </div>
          </summary>
          <div class="nhsd-m-expander__content-container">
            <span class="nhsd-t-body">

The MessageHeader resource carries information such as the sender and receiver as is a wrapper for the message. The event.system and event.code will match the MessageDefinition corresponding values. The definition element has a direct link to the MessageDefinition that will be used to check validation of the Bundle contents.             

### Application specific guidance for this resource:

@```
from Bundle
where id = 'bars-documentation-businesslevelguidance'
for entry where resource.id = 'servicerequestrequest-messageheader-111_ED'
	select *
	for resource.parameter
	select {
		FHIR_Element: name,
		Cardinality: min.toString() & '..' & max.toString(),
		Element_Values: documentation.split('|').first(),
		Additional_Guidance: documentation.split('|').tail()
	}

```
            </span>
          </div>
        </details>
      </div>
    </div>
  </div>
</div>
      
 

<hr>
