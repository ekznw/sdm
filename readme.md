# Species distribution modelling repository for KwaZulu-Natal

``` mermaid
---
config:
  layout: elk
  elk:
    padding: 25
    nodePlacement.strategy: SIMPLE
    spacing.nodeNode: 30
  themeVariables:
    primaryTextColor: "#ffffff"
    textColor: "#ffffff"
    labelTextColor: "#ffffff"
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
    
    EnvDataQuery -->|"Environmental<br/>variables"| EnvOverlay
    EnvDataQuery -->|"Environmental<br/>variables"| SDMAnalysis
    
    PointIntersection --> Output[Species<br/>Distribution<br/>Map]
    EnvOverlay --> Output
    SDMAnalysis --> Output
    
    Output --> PlanningUnits[Planning Units<br/>Layer]
    
    classDef database fill:#eef2ff,stroke:#818cf8
    classDef process fill:#f0fdf4,stroke:#4ade80
    classDef decision fill:#fff7ed,stroke:#fb923c
    classDef output fill:#fdf4ff,stroke:#e879f9
    
    class SpeciesRecordDB,EnvDataDB database
    class DataInput,SpeciesTraits,EnvDataQuery,PointIntersection,EnvOverlay,SDMAnalysis process
    class DecisionPoint decision
    class Output,PlanningUnits output
```

