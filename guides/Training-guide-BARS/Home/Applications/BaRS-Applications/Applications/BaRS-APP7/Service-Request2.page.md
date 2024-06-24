## {{page-title}}

Here is some placeholder text for the service request payload for this Application. Diagrams and other things can come here.


<div class="nhsd-o-expander-list">
<div class="nhsd-m-expander">
    <details>
        <summary class="nhsd-m-expander__heading-container" aria-label="Message Header" >
          <div>      
              <p class="nhsd-m-expander__heading nhsd-t-body">Message Header</p>
          </div>
        </summary>        
        <div class="nhsd-m-expander__content-container">
            <span class="nhsd-t-body">

This is the content inside an expander. It can contain text, images and other content by using the visual editor.

#### Business Level Guidance

<!-- update the resource.id value to pick the payload and resource to display -->
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
<div class="nhsd-m-expander">
    <details>
        <summary class="nhsd-m-expander__heading-container" aria-label="Service Request" >
          <div>      
              <p class="nhsd-m-expander__heading nhsd-t-body">Service Request</p>
          </div>
        </summary>
        <div class="nhsd-m-expander__content-container">
            <span class="nhsd-t-body">
                This is the content inside an expander. It can contain text, images and other content by using the visual editor.
            </span>      
        </div>
    </details> 
</div>

<div class="nhsd-m-expander">
    <details>
        <summary class="nhsd-m-expander__heading-container" aria-label="Healthcare Service" >
        <div>      
            <p class="nhsd-m-expander__heading nhsd-t-body">Healthcare Service</p>
        </div>
        </summary>
        <div class="nhsd-m-expander__content-container">
            <span class="nhsd-t-body">
                This is the content inside an expander. It can contain text, images and other content by using the visual editor.
            </span>      
        </div>
    </details> 
</div>

<div class="nhsd-m-expander">
    <details>
        <summary class="nhsd-m-expander__heading-container" aria-label="Encounter" >
        <div>      
            <p class="nhsd-m-expander__heading nhsd-t-body">Encounter</p>
        </div>
        </summary>
        <div class="nhsd-m-expander__content-container">
            <span class="nhsd-t-body">
                This is the content inside an expander. It can contain text, images and other content by using the visual editor.
            </span>      
        </div>
    </details> 
</div>

<div class="nhsd-m-expander">
    <details>
        <summary class="nhsd-m-expander__heading-container" aria-label="Care Plan" >
        <div>      
            <p class="nhsd-m-expander__heading nhsd-t-body">Care Plan</p>
        </div>
        </summary>
        <div class="nhsd-m-expander__content-container">
            <span class="nhsd-t-body">
                This is the content inside an expander. It can contain text, images and other content by using the visual editor.
            </span>      
        </div>
    </details> 
</div> 

<div class="nhsd-m-expander">
    <details>
        <summary class="nhsd-m-expander__heading-container" aria-label="Patient" >
        <div>      
            <p class="nhsd-m-expander__heading nhsd-t-body">Patient</p>
        </div>
        </summary>
        <div class="nhsd-m-expander__content-container">
            <span class="nhsd-t-body">
                This is the content inside an expander. It can contain text, images and other content by using the visual editor.
            </span>      
        </div>
    </details>  
</div>

<div class="nhsd-m-expander">
    <details>
        <summary class="nhsd-m-expander__heading-container" aria-label="Practitioner Role" >
        <div>      
            <p class="nhsd-m-expander__heading nhsd-t-body">Practitioner Role</p>
        </div>
        </summary>
        <div class="nhsd-m-expander__content-container">
            <span class="nhsd-t-body">
                This is the content inside an expander. It can contain text, images and other content by using the visual editor.
            </span>      
        </div>
    </details> 
</div> 

<div class="nhsd-m-expander">
    <details>
        <summary class="nhsd-m-expander__heading-container" aria-label="Practitioner" >
        <div>      
            <p class="nhsd-m-expander__heading nhsd-t-body">Practitioner</p>
        </div>
        </summary>
        <div class="nhsd-m-expander__content-container">
            <span class="nhsd-t-body">
                This is the content inside an expander. It can contain text, images and other content by using the visual editor.
            </span>      
        </div>
    </details> 
</div> 

<div class="nhsd-m-expander">
    <details>
        <summary class="nhsd-m-expander__heading-container" aria-label="Organization" >
        <div>      
            <p class="nhsd-m-expander__heading nhsd-t-body">Organization</p>
        </div>
        </summary>
        <div class="nhsd-m-expander__content-container">
            <span class="nhsd-t-body">
                This is the content inside an expander. It can contain text, images and other content by using the visual editor.
            </span>      
        </div>
    </details>  
</div>  

<div class="nhsd-m-expander">
    <details>
        <summary class="nhsd-m-expander__heading-container" aria-label="Medication Statement" >
        <div>      
            <p class="nhsd-m-expander__heading nhsd-t-body">Medication Statement</p>
        </div>
        </summary>
        <div class="nhsd-m-expander__content-container">
            <span class="nhsd-t-body">
                This is the content inside an expander. It can contain text, images and other content by using the visual editor.
            </span>      
        </div>
    </details>  
</div>

<div class="nhsd-m-expander">
    <details>
        <summary class="nhsd-m-expander__heading-container" aria-label="Allergy Intolerance" >
        <div>      
            <p class="nhsd-m-expander__heading nhsd-t-body">Allergy Intolerance</p>
        </div>
        </summary>
        <div class="nhsd-m-expander__content-container">
            <span class="nhsd-t-body">
                This is the content inside an expander. It can contain text, images and other content by using the visual editor.
            </span>      
        </div>
    </details>  
</div>

<div class="nhsd-m-expander">
    <details>
        <summary class="nhsd-m-expander__heading-container" aria-label="Flag" >
        <div>      
            <p class="nhsd-m-expander__heading nhsd-t-body">Flag</p>
        </div>
        </summary>
        <div class="nhsd-m-expander__content-container">
            <span class="nhsd-t-body">
                This is the content inside an expander. It can contain text, images and other content by using the visual editor.
            </span>      
        </div>
    </details>  
</div>

<div class="nhsd-m-expander">
    <details>
        <summary class="nhsd-m-expander__heading-container" aria-label="Questionnaire Response" >
        <div>      
            <p class="nhsd-m-expander__heading nhsd-t-body">Questionnaire Response</p>
        </div>
        </summary>
        <div class="nhsd-m-expander__content-container">
            <span class="nhsd-t-body">
                This is the content inside an expander. It can contain text, images and other content by using the visual editor.
            </span>      
        </div>
    </details>  
</div>

<div class="nhsd-m-expander">
    <details>
        <summary class="nhsd-m-expander__heading-container" aria-label="Observation" >
        <div>      
            <p class="nhsd-m-expander__heading nhsd-t-body">Observation</p>
        </div>
        </summary>
        <div class="nhsd-m-expander__content-container">
            <span class="nhsd-t-body">
                This is the content inside an expander. It can contain text, images and other content by using the visual editor.
            </span>      
        </div>
    </details>  
</div>

<div class="nhsd-m-expander">
    <details>
        <summary class="nhsd-m-expander__heading-container" aria-label="Consent" >
        <div>      
            <p class="nhsd-m-expander__heading nhsd-t-body">Consent</p>
        </div>
        </summary>
        <div class="nhsd-m-expander__content-container">
            <span class="nhsd-t-body">
                This is the content inside an expander. It can contain text, images and other content by using the visual editor.
            </span>      
        </div>
    </details>  
</div>
</div>
