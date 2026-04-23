---
title: "Direct Air Capture (DAC) | Ionic Stacks"
date: 2026-03-31
showDate: false
showSummaryDate: false
showReadingTime: false
showSummaryReadingTime: false
showWordCount: false
showPagination: false
showTaxonomies: false
showTableOfContents: false
layout: "simple"
description: "Electrochemical DAC systems."
---

The air around us contains an average of 425 ppm (0.0425 vol%) of CO<sub>2</sub>. This dilute concentration is precisely why DAC represents one of the greatest engineering challenges in climate tech: it is an absolute uphill battle against thermodynamics. While conventional carbon capture relies on heat for the regeneration process, electrochemistry can drive the separation using electrons, allowing the system to operate entirely on a renewable grid.

---
## pH-Swing Architecture
The behaviour of CO<sub>2</sub> is determined by the acidity (pH) of its environment. In an alkaline solvent, CO<sub>2</sub> is captured and held in a stable, dissolved state (as bicarbonate, carbonate, or carbamate ions). The electrochemical stack uses electricity to simultaneously generate acidic and alkaline conditions to shift this balance. The acid is used to release a CO<sub>2</sub> as a concentrated gas, while the base regenerates the capture solvent so that it can loop back to the air contactor and capture more CO<sub>2</sub>.

<div style="max-width: 850px; margin: 0 auto;">

{{<mermaid >}}
  flowchart LR

  %% define the nodes
    Ambient[/"Ambient Air"/]
    Contactor["Air Contactor"]
    Clean[/"CO₂-Clean Air"/]
    Pure[/"High-Purity CO₂"/]
    Stack[["Stack"]]
    

  %% define the flow
    Ambient --> Contactor
    Contactor --> Clean
    Contactor --> |CO₂-Rich| Stack
    Stack --> |CO₂-Lean| Contactor
    Stack --> Pure

   %% styling
    classDef StackStyle padding:25px 50px,stroke-width:4px,font-weight:bold,font-size:18px;
    class Stack StackStyle

{{</mermaid >}}

</div>

---
## Electro-Swing Architecture
These electrodes are like "switchable CO<sub>2</sub> magnets." Rather than circulating liquid electrolytes, this architecture relies on redox-active electrodes that change their chemical affinity based on the applied voltage. The system captures CO<sub>2</sub> while in a reduced state and releases it in an oxidized state when the polarity is reversed.

<div style="max-width: 550px; margin: 0 auto;">
  
{{<mermaid >}}
  flowchart LR

  %% define the nodes
    Ambient[/"Ambient Air"/]
    Clean[/"CO₂-Clean Air"/]
    Stack[["Stack"]]
    Pure[/"High-Purity CO₂"/]

  %% define the flow
    Ambient --> Stack
    Stack --> Clean
    Stack --> Pure

   %% styling
    classDef StackStyle padding:25px 50px,stroke-width:4px,font-weight:bold,font-size:18px;
    class Stack StackStyle

{{</mermaid >}}

</div>

---
{{<list title="Sifting the Skies" cardView=true limit=6 where="Params.list_type" value="dac">}}