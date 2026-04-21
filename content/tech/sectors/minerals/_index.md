---
title: "Minerals"
date: 2026-03-30
showDate: false
showSummaryDate: false
showReadingTime: false
showSummaryReadingTime: false
showWordCount: false
showPagination: false
showTaxonomies: false
layout: simple
description: "electrochemical mineral extraction and cement mineralization"
---

---
## Direct Lithium Extraction (DLE)

<div style="max-width: 900px; margin: 0 auto;">

{{<mermaid >}}
  flowchart LR

  %% define the nodes
    Brine[/"Brine"/]
    Water[/"Water"/]
    Stack[["Stack"]]
    Outflow[/"Concentrated Li<sup>+</sup> Solution"/]
    Spent[/"Spent Brine"/]
    Purification["Purification"]
    Pure[/"Lithium Solids"/]

  %% define the flow
    Brine --> Stack
    Water --> Stack
    Stack --> Outflow
    Stack --> Spent
    Outflow --> Purification
    Purification --> Pure

   %% styling
    classDef StackStyle padding:25px 50px,stroke-width:4px,font-weight:bold,font-size:18px;
    class Stack StackStyle
{{</mermaid >}}

</div>

---
## Electrochemical Salt Splitting

<div style="max-width: 900px; margin: 0 auto;">

{{<mermaid >}}
  flowchart LR

  %% define the nodes
    Salt[/"Salt Solution / Brine"/]
    Stack[["Stack"]]
    Recovery["Acid Leaching <br/>&<br/> Base Precipitation"]
    Pure[/"Mineral Solids"/]

  %% define the flow
    Salt --> Stack
    Stack --> |Acidic Stream|Recovery
    Stack --> |Alkaline Stream|Recovery
    Recovery --> Pure

   %% styling
    classDef StackStyle padding:25px 50px,stroke-width:4px,font-weight:bold,font-size:18px;
    class Stack StackStyle
{{</mermaid >}}

</div>