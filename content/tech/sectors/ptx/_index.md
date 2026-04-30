---
title: "Power-to-X (PtX)"
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
description: "Sustainable power-to-x pathways."
---
{{< katex >}}

Our world today is built on a foundation of chemicals and fuels. Traditionally, these products originate from fossil feedstocks and are synthesized in energy-intensive, thermochemical reactors operating at high temperatures and pressures. Power-to-X (PtX) answers the question: **How do we sustainably meet the energy and material demands of a modernizing world?** From feedstocks to energy inputs, PtX is the shift from thermochemical to electrochemical systems that rely on water, captured CO<sub>2</sub>, and renewable electricity. PtX plays a key part in broad decarbonization efforts, producing eChemicals and eFuels for hard-to-abate sectors, such as aviation, shipping, steel production, and chemical manufacturing, where high energy density remains essential.

<div style="max-width: 650px; margin: 0 auto;">
  
{{<mermaid >}}
  flowchart LR

  %% define the nodes
    Water[/"Water (H₂O)"/]
    CO2[/"Carbon Dioxide (CO₂)"/]
    Stack[["Stack"]]
    Hydrogen[/"Hydrogen (H₂)"/]
    Syngas[/"Syngas (H₂ + CO)"/]
    Cprod[/"Carbon-Based Products"/]

  %% define the flow
    Water --> Stack
    CO2 --> Stack
    Stack --> Hydrogen
    Stack --> Syngas
    Stack --> Cprod

   %% styling
    classDef StackStyle padding:25px 50px,stroke-width:4px,font-weight:bold,font-size:18px;
    class Stack StackStyle

{{</mermaid >}}

</div>

---
## Green Hydrogen (H<sub>2</sub>)
The most mature "X" is H<sub>2</sub>. In an electrochemical stack, H<sub>2</sub> is generated at the cathode through the hydrogen evolution reaction (HER):

<div style="margin: 0 auto; text-align: center;">
\(2H^+ + 2e^- \rightarrow H_2\)
</div>

H<sub>2</sub> is a versatile and powerful molecule. It can be used directly as a fuel for heavy-duty transport or as a reducing agent in steel manufacturing to replace carbon-heavy coke. It is also an essential feedstock for industrial processes such as green ammonia production, where H<sub>2</sub> is combined with atmospheric nitrogen to synthesize sustainable fertilizers via the Haber-Bosch process.

---
## Carbon Dioxide (CO<sub>2</sub>) Valorization
CO<sub>2</sub> electrolysis uses electricity to "reverse combustion" through the CO<sub>2</sub> reduction reaction (CO<sub>2</sub>RR). The most industrially viable product is carbon monoxide (CO), which can be combined with green H<sub>2</sub> to form synthesis gas (syngas) and used as a feedstock in the Fischer-Tropsch process to produce sustainable aviation fuel (SAF) or synthetic diesel.

<div style="margin: 0 auto; text-align: center;">
\(CO_2 + 2H^+ + 2e^- \rightarrow CO + H_2O\)
</div>

CO<sub>2</sub> electrolysis can also generate multi-carbon (C<sub>2+</sub>) products such as ethylene (C<sub>2</sub>H<sub>4</sub>), a building block for the global plastics industry, and ethanol (C<sub>2</sub>H<sub>5</sub>OH), a high-energy density fuel additive, versatile industrial solvent, and ingredient of alcoholic beverages.

<div style="margin: 0 auto; text-align: center;">
\(2CO_2 + 12H^+ + 12e^- \rightarrow C_2H_4 + 4H_2O\)

\(2CO_2 + 12H^+ + 12e^- \rightarrow C_2H_5OH + 3H_2O\)
</div>

---
{{<list title="Sparking the Stock" cardView=true limit=6 where="Params.list_type" value="ptx">}}