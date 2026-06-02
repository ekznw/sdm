# Species distribution modelling repository for KwaZulu-Natal

``` mermaid
---
config:
  layout: elk
  elk:
    nodePlacement.strategy: SIMPLE
    padding: 25
    spacing.nodeNode: 50         # ↑ increase node spacing
    spacing.nodeNodeBetweenLayers: 50
  themeVariables:
    primaryTextColor: "#322c2c"       # arrow labels
    textColor: "#312709"              # node text
    labelTextColor: "#151319"         # node labels
    lineColor: "#e69d1e"              # arrow color
    edgeLabelBackground: "#e2c888bf"  # link bg color
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
    
    classDef database fill:#618571,stroke:#9da19f
    classDef process fill:#dda381,stroke:#909592
    classDef decision fill:#fde68a,stroke:#fb923c
    classDef output fill:#618571,stroke:#9da19f
    
    class SpeciesRecordDB,EnvDataDB database
    class DataInput,SpeciesTraits,EnvDataQuery,PointIntersection,EnvOverlay,SDMAnalysis process
    class DecisionPoint decision
    class Output,PlanningUnits output
```

