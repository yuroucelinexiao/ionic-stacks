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
description: "Electrochemical DAC systems."
---

The air around us contains an average of 425 ppm (0.0425 vol%) of CO&#8322;. While this may not sound like much, it is precisely why DAC represents one of the greatest engineering challenges in climate tech: it is an absolute uphill battle against thermodynamics. While conventional carbon capture relies on heat for the regeneration process, electrochemistry can drive the separation using electrons, allowing the system to operate entirely on a renewable grid.

---
### pH-Swing Architecture
When CO&#8322; (an acid) is captured by a highly alkaline solvent (a base) in an air contactor, it transforms into an ionic form, generating a CO₂-rich solution. The electrochemical stack then drives the cycle by shifting the pH down to trigger the release of concentrated CO&#8322;, then shifting it back up to regenerate the solvent. This returns a CO&#8322;-lean solution to the air contactor and completes the loop.

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

---
### Electro-Swing Architecture
These electrodes are like "switchable CO&#8322; magnets." Rather than circulating liquid electrolytes, this architecture relies on redox-active electrodes that change their chemical affinity based on the applied voltage. The system captures CO&#8322; while in a reduced state and releases it in an oxidized state when the polarity is reversed.

<div style="max-width: 365px; margin: 0 auto;">

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
