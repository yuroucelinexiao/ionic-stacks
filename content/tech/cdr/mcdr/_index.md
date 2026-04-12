---
title: "Marine Carbon Dioxide Removal (mCDR)"
date: 2026-03-30
showDate: false
showSummaryDate: false
showReadingTime: false
showSummaryReadingTime: false
showWordCount: false
showPagination: false
showTaxonomies: false
showTableOfContents: false
layout: "simple"
description: "Electrochemical mCDR systems."
---
The ocean is a massive carbon sink. Covering ~71% of the Earth's surface, it acts as the world's largest air contactor that absorbs CO<sub>2</sub> from the atmosphere in an attempt to maintain an equilibrium. Ocean surface water contains on average ~2 mM of dissolved inorganic carbon (DIC)—CO<sub>2</sub> in its various chemical states, including aqueous CO<sub>2</sub>, carbonic acid, bicarbonate, and carbonate ions. Excess CO<sub>2</sub> acidifies the ocean, pushing this natural buffer to its limits and threatening marine ecosystems. The goal of mCDR is to restore this delicate balance by either extracting the dissolved carbon or permanently expanding the ocean's safe absorption capacity.

---

### Direct Ocean Capture (DOC)

Electrochemical DOC relies on the ocean's natural carbonate equilibrium. The electrochemical stack uses electricity to split the incoming seawater to generate acids and bases. When the seawater pH is shifted down using the acidic stream, the DIC is extracted as a concentrated CO<sub>2</sub> gas stream. The DIC-depleted water is then recombined with the alkaline stream to rebalance the pH and returned to the ocean. 

<div style="max-width: 700px; margin: 0 auto;">

{{<mermaid >}}
  flowchart LR

  %% define the nodes
    Intake[/"Intake Seawater"/]
    Stack[["Stack"]]
    Pure[/"High-Purity CO<sub>2</sub>"/]
    Outflow[/"Outflow Seawater"/]

  %% define the flow
    Intake -->|DIC-Rich| Stack
    Stack --> Pure
    Stack -->|DIC-Depleted| Outflow

   %% styling
    classDef StackStyle padding:25px 50px,stroke-width:4px,font-weight:bold,font-size:18px;
    class Stack StackStyle
{{</mermaid >}}

</div>

---
### Ocean Alkalinity Enhancement (OAE)

OAE doesn't involve any CO<sub>2</sub> handling. Instead, this approach focuses on expanding the ocean's CO<sub>2</sub> absorption capacity. The electrochemical stack splits seawater or waste brine into an alkaline stream for ocean discharge and an acidic stream for use in other processes. The added alkalinity shifts the carbonate equilibrium in the ocean, converting dissolved aqueous CO<sub>2</sub> into bicarbonates, and restoring the ocean's natural buffering capacity.

<div style="max-width: 700px; margin: 0 auto;">

{{<mermaid >}}
flowchart LR

  %% define the nodes
    Intake[/"Intake Seawater / Brine"/]
    Stack[["Stack"]]
    Outflow[/"Outflow Seawater"/]
    Acid[/"Acid Valorization"/]

  %% define the flow
    Intake --> Stack
    Stack --> |Acidic Stream|Acid
    Stack --> |Alkaline Stream|Outflow

   %% styling
    classDef StackStyle padding:25px 50px,stroke-width:4px,font-weight:bold,font-size:18px;
    class Stack StackStyle
{{</mermaid >}}

</div>

---
{{<list title="Scrubbing the Seas" cardView=true limit=6 where="Params.list_type" value="mcdr">}}