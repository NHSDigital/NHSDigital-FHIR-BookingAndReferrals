<div class="nhsd-t-grid nhsd-!t-margin-top-8">
	<div class="nhsd-t-row nhsd-!t-margin-bottom-3">
		<div class="nhsd-t-col-12">
			<nav class="nhsd-m-tabs">
				<div role="tablist">    
					<a class="nhsd-a-tab" href="#content-1" id="tab-content-1" data-tab-content="content-1" aria-controls="content-1"aria-selected="false" role="tab">Diff</a>
					<a class="nhsd-a-tab" href="#content-2" id="tab-content-2" data-tab-content="content-2" aria-controls="content-2"aria-selected="false" role="tab">Hybrid</a>
					<a class="nhsd-a-tab" href="#content-3" id="tab-content-3" data-tab-content="content-3" aria-controls="content-3"aria-selected="false" role="tab">Snapshot</a>
					<hr class="nhsd-a-horizontal-rule nhsd-a-horizontal-rule--size-xxs" />
				</div>
			</nav>
		</div>
	</div>
    <div id="content-1" class="nhsd-t-row nhsd-!t-margin-top-3" role="tabpanel" aria-hidden="true" aria-labelledby="tab-content-1">
		<div class="nhsd-t-col-12">
			<p data-hide-tab-header class="nhsd-t-heading-l">FHIR model diff view</p>
{{tree:https://fhir.nhs.uk/MessageDefinition/bars-message-servicerequest-request-referral, diff}}
		</div>
	</div>
	<div id="content-2" class="nhsd-t-row nhsd-!t-margin-top-3" role="tabpanel" aria-hidden="true" aria-labelledby="tab-content-2">
		<div class="nhsd-t-col-12">
			<p data-hide-tab-header class="nhsd-t-heading-l">FHIR model hybrid view</p>
{{tree:https://fhir.nhs.uk/MessageDefinition/bars-message-servicerequest-request-referral, hybrid}}
		</div>
	</div>
	<div id="content-3" class="nhsd-t-row nhsd-!t-margin-top-3" role="tabpanel" aria-hidden="true" aria-labelledby="tab-content-3">
		<div class="nhsd-t-col-12">
			<p data-hide-tab-header class="nhsd-t-heading-l">FHIR model snapshot view</p>
			{{tree:https://fhir.nhs.uk/MessageDefinition/bars-message-servicerequest-request-referral, snapshot}}
		</div>
	</div>
</div>