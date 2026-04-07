---
title: "Direct Air Capture (DAC)"
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

The air around us contains an average of 425 ppm (0.0425 vol%) of CO&#8322;. This dilute concentration is precisely why DAC represents one of the greatest engineering challenges in climate tech: it is an absolute uphill battle against thermodynamics. While conventional carbon capture relies on heat for the regeneration process, electrochemistry can drive the separation using electrons, allowing the system to operate entirely on a renewable grid.

---
### pH-Swing Architecture
The behaviour of CO&#8322; is determined by the acidity (pH) of its environment. In an alkaline solvent, CO&#8322; is captured and held in a stable, dissolved state. The electrochemical stack uses electricity to simultaneously generates acidic and alkaline conditions to shift this balance. The acid is used to release a CO&#8322; as a concentrated gas, while the base regenerates the capture solvent so that it can capture more CO&#8322;, completing the loop.

<div style="max-width: 700px; margin: 0 auto;">

{{<mermaid >}}
  flowchart LR

  %% define the nodes
    Ambient[/"Ambient Air"/]
    Contactor["Air Contactor"]
    Stack[["Stack"]]
    Pure[/"High-Purity CO&#8322;"/]

  %% define the flow
    Ambient --> Contactor
    Contactor -->|CO&#8322;-Rich| Stack
    Stack --> |CO&#8322;-Lean| Contactor
    Stack --> Pure

   %% styling
    classDef StackStyle padding:25px 50px,stroke-width:4px,font-weight:bold,font-size:18px;
    class Stack StackStyle

{{</mermaid >}}

</div>

---
### Electro-Swing Architecture
These electrodes are like "switchable CO&#8322; magnets." Rather than circulating liquid electrolytes, this architecture relies on redox-active electrodes that change their chemical affinity based on the applied voltage. The system captures CO&#8322; while in a reduced state and releases it in an oxidized state when the polarity is reversed.

<div style="max-width: 450px; margin: 0 auto;">

{{<mermaid >}}
  flowchart LR

  %% define the nodes
    Ambient[/"Ambient Air"/]
    Stack[["Stack"]]
    Pure[/"High-Purity CO&#8322;"/]

  %% define the flow
    Ambient --> Stack
    Stack --> Pure

   %% styling
    classDef StackStyle padding:25px 50px,stroke-width:4px,font-weight:bold,font-size:18px;
    class Stack StackStyle

{{</mermaid >}}

</div>

---
{{<list title="Sifting the Skies" cardView=true limit=6 >}}