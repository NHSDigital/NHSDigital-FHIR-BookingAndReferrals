---
topic: core-FHIRUsage-JourneyID-1.1.3
---

## {{page-title}}

The Journey ID uses the episodeOfCare resource.

Each Encounter between systems can reference the same originating episodeOfCare, allowing grouping of all the Encounters to one flow.

The FHIR episodeOfCare resource would be created at the beginning of the patient journey when the Encounter is created and leads onto a ServiceRequest or other appropriate flow.

{{render:Encounter-episodeOfCare-screenshot}}

This snippet of coding shows the episodeOfCare within the Encounter referencing a GUID that will be used throughout the patients journey.

```xml 
<episodeOfCare>
    <!--      Resource reference to an EpisodeOfCare Journey ID      -->
    <reference value="d877b820-e72b-44d1-a627-195f54bfc606" />
</episodeOfCare>
```

<br>
<hr>