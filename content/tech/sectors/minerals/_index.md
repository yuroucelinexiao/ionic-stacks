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

Critical minerals, such as lithium, nickel, cobalt, and rare earth elements, are essential components in modern batteries and high-performance electronics. These industries are resource-intensive, but they are also the powerhouses of the global energy transition. However, extracting these minerals from the Earth’s crust has become increasingly difficult and expensive as high-grade ore deposits are depleted. Electrochemistry offers a sustainable pathway to extract and recover these minerals from unconventional sources, including brines, industrial wastewater, and spent batteries.

---
## Direct Lithium Extraction (DLE)

Electrochemical DLE relies on electro-swing adsorption. It uses electrical potentials to drive lithium ions (Li<sup>+</sup>) into selective, redox-active electrodes. Once the electrode reaches capacity, the polarity is reversed to release the Li<sup>+</sup> into a release electrolyte. This enriched stream is then concentrated and the lithium is precipitated as high-purity solids.

<div style="max-width: 850px; margin: 0 auto;">

{{<mermaid >}}
  flowchart LR

  %% define the nodes
    Brine[/"Brine"/]
    Release[/"Release Electrolyte"/]
    Stack[["Stack"]]
    Outflow[/"Concentrated Li⁺ Solution"/]
    Spent[/"Spent Brine"/]
    Pure[/"Lithium Solids"/]

  %% define the flow
    Brine --> Stack
    Release --> Stack
    Stack --> Outflow
    Stack --> Spent
    Outflow --> Pure

   %% styling
    classDef StackStyle padding:25px 50px,stroke-width:4px,font-weight:bold,font-size:18px;
    class Stack StackStyle
{{</mermaid >}}

</div>

---
## Electrochemical Salt Splitting

The electrochemical stack splits salt solutions into concentrated acidic and alkaline streams. The acid is used to leach target minerals from secondary feedstocks, such as battery black mass or mining tailings, while the base is used to selectively precipitate these minerals as solids. After the mineral recovery process, the resulting neutralized salt solution is returned to the stack, closing the loop.

<div style="max-width: 900px; margin: 0 auto;">

{{<mermaid >}}
  flowchart LR

  %% define the nodes
    Salt[/"Salt Solution"/]
    Stack[["Stack"]]
    Recovery["Acid Leaching <br/>&<br/> Base Precipitation"]
    Pure[/"Mineral Solids"/]

  %% define the flow
    Salt --> Stack
    Stack --> |Acidic Stream|Recovery
    Stack --> |Alkaline Stream|Recovery
    Recovery --> Pure
    Recovery --> Salt

   %% styling
    classDef StackStyle padding:25px 50px,stroke-width:4px,font-weight:bold,font-size:18px;
    class Stack StackStyle
{{</mermaid >}}

</div>