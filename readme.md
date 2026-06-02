# Species distribution modelling repository for KwaZulu-Natal

``` mermaid
---
---
config:
  layout: elk
  elk:
    algorithm: layered
    nodePlacement.strategy: SIMPLE
    padding: 25
    spacing.nodeNode: 60
    spacing.nodeNodeBetweenLayers: 80
  themeVariables:
    primaryTextColor: "#322c2c"
    textColor: "#312709"
    labelTextColor: "#151319"
    lineColor: "#e69d1e"
    edgeLabelBackground: "#e2c888bf"
---
flowchart TD
    SpeciesRecordDB[(Species Record<br/>Database)] -->|Pull species<br/>occurrence data| DataInput[Species<br/>Occurrence Data]
    DataInput --> DecisionPoint{Decision:<br/>Analysis Type}
    
    DecisionPoint -->|Option 1:<br/>Simple intersection| PointIntersection[Point Intersection<br/>with Planning Units]
    DecisionPoint -->|Option 2:<br/>Environmental<br/>overlay| EnvOverlay[Environmental<br/>Overlay Analysis]
    DecisionPoint -->|Option 3:<br/>Full<br/>modelling| SDMAnalysis[Species Distribution<br/>Model Analysis]
    
    SpeciesRecordDB -->|Query species<br/>traits & groups| SpeciesTraits[Species Traits<br/>& Group Data]
    SpeciesTraits --> EnvDataQuery[Query Environmental<br/>Data by Species<br/>Traits/Groups]
    
    EnvDataDB[(Environmental Data<br/>Database)] -->|Fetch layers:<br/>climate, soil,<br/>vegetation| EnvDataQuery
    
    %% Spacer node to prevent overlap between Option 3 and Environmental variables links
    EnvDataQuery --> EnvSpacer((" ")):::spacer
    EnvSpacer -->|"Environmental<br/>variables"| EnvOverlay
    EnvSpacer -->|"Environmental<br/>variables"| SDMAnalysis
    
    PointIntersection --> Output[Species<br/>Distribution<br/>Map]
    EnvOverlay --> Output
    SDMAnalysis --> Output
    
    Output --> PlanningUnits[Planning Units<br/>Layer]
    
    classDef database fill:#618571,stroke:#9da19f
    classDef process fill:#dda381,stroke:#909592
    classDef decision fill:#fde68a,stroke:#fb923c
    classDef output fill:#618571,stroke:#9da19f
    classDef spacer fill:none,stroke:none
    
    class SpeciesRecordDB,EnvDataDB database
    class DataInput,SpeciesTraits,EnvDataQuery,PointIntersection,EnvOverlay,SDMAnalysis process
    class DecisionPoint decision
    class Output,PlanningUnits output
    class EnvSpacer spacer
```

