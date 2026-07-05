---
title: "Salt splitting in a diaphragm cell for battery recycling"
date: 2026-05-16
list_type: "minerals"
draft: false
showWordCount: false
showTableOfContents: true
showHero: true
heroStyle: background
summary: "battery-recycling-diaphragm-cell"
categories: ["Minerals Deep Dive"]
tags: ["Li-ion battery", "LIB", "Recycling", "Salt splitting", "Diaphragm", "Current efficiency", "Concentration"]
---
{{< katex >}}

## Battery recycling for critical metals recovery
The increase in demand for electric vehicles and grid-scale storage has rapidly expanded the production of lithium-ion batteries (LIBs). To keep up the **supply of critical metals** (e.g. lithium, cobalt, and nickel) and to **reduce waste**, LIB recycling processes have also significantly expanded. Spent LIBs, which contain a much **higher concentration of valuable metals** than brines and ores, can be recycled through direct regeneration, pyrometallurgy, hydrometallurgy, or a combination of methods[^1].
- **Direct:** The composition and structure of the degraded cathode material can be restored by introducing a lithium source through calcination. This method offers the lowest energy consumption and cost, but is bottlenecked by high requirements for feedstock purity and sorting.
- **Pyrometallurgy:** Batteries are smelted at high temperatures to recover the critical metals as alloys. This method can handle a wide range of battery feedstocks with minimal pre-processing, but uses massive amounts of energy and produces toxic gases in the process.
- **Hydrometallurgy:** Strong acids are used to dissolve the spent cathode material, and bases are used to selectively precipitate and recover the valuable metals. This method achieves high metal recovery rates with low energy consumption, but requires intensive chemical inputs and generates large amounts of wastewater and salt.

## Electrochemical salt splitting for hydrometallurgy
Electrolyzers split salt water, a byproduct of hydrometallurgy, into the acids and bases needed for battery recycling. Misleh et al. recently demonstrated recycling of lithium cobalt oxide (LCO) and lithium nickel manganese cobalt oxide (NMC) cathodes using acids and bases electrochemically generated from lithium sulfate (Li<sub>2</sub>SO<sub>4</sub>) in a **diaphragm flow cell**[^2].

In an electrolyzer, the cathode and anode are isolated using an ion exchange membrane or a porous physical barrier (e.g. a diaphragm). These electrochemical separators **prevent the mixing of gases** and **electrically insulate** the two electrodes while allowing **ionic transport** to maintain charge balance across the cell.

### Ion exchange membranes
Ion exchange membranes (IEMs) are polymer sheets that contain a **high concentration of fixed charges**. It relies on **electrostatic forces** to selectively allow only ions of either positive or negative charges through. IEMs offer **high current efficiency** (i.e., fraction of target ions versus total ions that cross the membrane) and can yield high purity products. However, they are expensive, delicate, sensitive to operational conditions, and have high internal resistances that increase the operating voltage.

**Anion exchange membranes (AEMs)** are fixed with positive charges (e.g. quaternary ammonium groups, imidazolium-based cations) and will allow the transport of hydroxide ions (OH<sup>-</sup>) and sulfate ions (SO<sub>4</sub><sup>2-</sup>) from the cathode to the anode while blocking protons (H<sup>+</sup>) and lithium ions (Li<sup>+</sup>).

<div style="max-width: 200px; margin: 0 auto;">

{{<mermaid >}}
  flowchart RL

  %% define the nodes
    Stack[["→OH<sup>-</sup>→ <br/>
            AEM </br>
            →SO<sub>4</sub><sup>2-</sup>→ </br>"]]
    Proton((H<sup>+</sup>))
    Lithium((Li<sup>+</sup>))

  %% define the flow
    Proton --> |<strong>X</strong>|Stack
    Lithium --> |<strong>X</strong>|Stack

   %% styling
    classDef StackStyle padding:25px 50px,stroke-width:4px,font-weight:bold,font-size:18px;
    class Stack StackStyle
{{</mermaid >}}

</div>

**Cation exchange membranes (CEMs)** are fixed with negative charges (e.g. sulfonate groups, carboxylate groups) and will allow the transport of H<sup>+</sup> and Li<sup>+</sup> from the anode to the cathode while blocking OH<sup>-</sup> and SO<sub>4</sub><sup>2-</sup>.

<div style="max-width: 200px; margin: 0 auto;">

{{<mermaid >}}
  flowchart LR

  %% define the nodes
    Stack[["←H<sup>+</sup>← <br/>
            CEM </br>
            ←Li<sup>+</sup>← </br>"]]
    Hydroxide((OH<sup>-</sup>))
    Sulfate((SO<sub>4</sub><sup>2-</sup>))

  %% define the flow
    Hydroxide --> |<strong>X</strong>|Stack
    Sulfate --> |<strong>X</strong>|Stack

   %% styling
    classDef StackStyle padding:25px 50px,stroke-width:4px,font-weight:bold,font-size:18px;
    class Stack StackStyle
{{</mermaid >}}

</div>

Misleh et al. noted that IEMs exhibit high cell resistance and susceptibility to fouling, and therefore pivoted to a diaphragm flow cell.

### Diaphragms
Diaphragms feature macro- or nanospores that completely fill up with electrolyte and allow **rapid, liquid-phase transport of ions** between electrodes. This greatly reduces the cell resistance. However, due to the lack of charge selectivity, diaphragms struggle with achieving high current efficiency and producing high purity products.

<div style="max-width: 200px; margin: 0 auto;">

{{<mermaid >}}
  flowchart LR

  %% define the nodes
    Stack[["←H<sup>+</sup>, Li<sup>+</sup>← <br/>
            Diaphragm </br>
            →OH<sup>-</sup>, SO<sub>4</sub><sup>2-</sup>→"]]
  
   %% styling
    classDef StackStyle padding:25px 50px,stroke-width:4px,font-weight:bold,font-size:18px;
    class Stack StackStyle
{{</mermaid >}}

</div>

## High current efficiency in diaphragm cells
Electrochemically splitting Li<sub>2</sub>SO<sub>4</sub> produces acidic lithium bisulfate (LiHSO<sub>4</sub>) at the anode by locally generating H<sup>+</sup> and basic lithium hydroxide (LiOH) at the cathode by locally generating OH<sup>-</sup>. To **prevent the recombination of acid and base**, the concentration of the Li<sub>2</sub>SO<sub>4</sub> supporting electrolyte was kept high at 2 M to **outcompete the crossover** of the acid and base across the non-selective diaphragm.

### All about concentration
Managing the concentration of the acid in the anolyte and the base in the catholyte is the key to reducing unwanted ion migration.
- **Acid concentration ([H<sup>+</sup>]) in anolyte:** The battery recycling process needs highly concentrated acid streams (0.6–3.0 M) for industrially relevant pulp densities (20–100 grams of cathode material per litre). High acid concentrations reduce the current efficiency due to the driving force of a large concentration gradient. The SO<sub>4</sub><sup>2-</sup> buffers the system by converting locally produced H<sup>+</sup> into HSO<sub>4</sub><sup>-</sup>, effectively trapping the protons and restricting their miggration towards the cathode.
- **Catholyte-to-anolyte flow ratio:** Unlike the acid stream, strong bases are not needed because the precipitation reactions are thermodynamically favourable even at lower concentrations. Therefore, the catholyte flow rate can be increased to dilute the OH<sup>-</sup> concentration and reduce its crossover.
- **Cell operating temperature:** Higher temperatures increase the formation of LiOH contact ion pairs, which effectively lowers the concentration of free OH<sup>-</sup> and reduces the solution pH, minimizing crossover. The operating voltage also decreases at elevated temperatures.

### Try the slider
Use the sliders below to see how adjusting each lever impacts current efficiency.

<div style="background: #0B3A46; padding: 25px; border-radius: 12px; border: 1px solid #A6A6A6; color: white; font-family: sans-serif; max-width: 700px; margin: 0 auto;">
  
  <h3 style="margin-top: 0; color: #B89C3F; border-bottom: 1px solid rgba(255,255,255,0.1); padding-bottom: 10px;">Diaphragm flow cell current efficiency</h3>

  <label>Acid concentration ([H<sup>+</sup>]) in anolyte: <strong id="acid-val" style="color: #B89C3F;">1.00</strong> M </label>
  <input type="range" id="acid-slider" min="0.6" max="3.0" step="0.1" value="1.00" style="width: 100%; margin-top: 20px; accent-color: #B89C3F;">

  <label>Catholyte-to-anolyte flow ratio: <strong id="flow-val" style="color: #B89C3F;">2.0</strong> : 1 </label>
  <input type="range" id="flow-slider" min="1.0" max="5.0" step="0.1" value="2.0" style="width: 100%; margin-top: 20px; accent-color: #B89C3F;">

  <label>Cell operating temperature: <strong id="temp-val" style="color: #B89C3F;">25</strong> °C </label>
  <input type="range" id="temp-slider" min="20" max="70" step="1" value="25" style="width: 100%; margin-top: 20px; accent-color: #B89C3F;">

  <div style="background: white; padding: 15px; border-radius: 8px; text-align: center; margin-top: 20px;">
    <span style="font-size: 16px; color: grey; text-transform: uppercase; letter-spacing: 1px;">Current Efficiency</span><br>
    <span id="ce-val" style="font-size: 36px; font-weight: bold; color: #B89C3F;">59.8</span>
    <span style="font-size: 24px; color: #B89C3F;"> %</span><br>
  </div>

</div>

<script>
  const acidSlider = document.getElementById('acid-slider');
  const flowSlider = document.getElementById('flow-slider');
  const tempSlider = document.getElementById('temp-slider');

  const acidVal = document.getElementById('acid-val');
  const flowVal = document.getElementById('flow-val');
  const tempVal = document.getElementById('temp-val');

  const ceOutput = document.getElementById('ce-val');

  // limiting molar ionic conductivity at 25C per unit charge
  const u_H_base = 349.6;
  const u_OH_base = 198.6; 
  const u_Li_base = 38.7;
  const u_SO4_base = 79.8;

  const conc_Li = 4;   
  const conc_SO4 = 2;  

  // Vogel-Fulcher-Tammann (VFT) emperical model for viscosity vs. temperature for concentrated electrolytes
  function getViscosity(tempC) {
    const tempK = tempC + 273.15;
    return 1.57e-5 * Math.pow(10, 311.2 / (tempK - 135));
  }
  const viscosity25 = getViscosity(25);

  // Calculate CE vs each lever
  function calculateCE() {
    const acidConc = parseFloat(acidSlider.value); 
    const flowRatio = parseFloat(flowSlider.value);
    const tempC = parseFloat(tempSlider.value);

    // Calculate Lever 3: Temperature scaling
    const currentViscosity = getViscosity(tempC);
    const viscosityRatio = viscosity25 / currentViscosity;
    const u_Li = u_Li_base * viscosityRatio;
    const u_SO4 = u_SO4_base * viscosityRatio;
    const u_H = u_H_base * Math.pow(viscosityRatio, 0.75); // Protons use mostly Grotthuss mechanism (hopping) and will scale slightly less than purely vehicular ions

    // Calculate Lever 1: Acid concentration
    const z_H = 1, z_Li = 1, z_SO4 = 2;
    const totalConductivityDenom = (z_H * u_H * acidConc) + (z_Li * u_Li * conc_Li) + (z_SO4 * u_SO4 * conc_SO4);
    const t_H_baseline = (z_H * u_H * acidConc) / totalConductivityDenom; // Baseline proton transference number

    // Calculate Lever 2: Flowrate ratio
    const R = 8.314;
    const F = 96485;
    const tempK = tempC + 273.15;
    const D_H = (u_H * 1e-4 * R * tempK) / (z_H * Math.pow(F, 2));
    const poreLength = 0.0005; // Industrial benchmark pore length (500 um) for non-selective diaphragms
    const baselineVelocity = 1e-6; 
    const linearVelocity = flowRatio * baselineVelocity;
    const Pe = (linearVelocity * poreLength) / D_H; // Péclet Number (ratio of advective transport to diffusive transport): Pe = (v * L) / D
    const m_flow = Pe > 1e-4 ? Pe / (Math.exp(Pe) - 1) : 1.0;
    const t_H_adjusted = t_H_baseline * m_flow;

    // Output
    const currentEfficiency = Math.min(100, Math.max(0, 100 * (1.0 - t_H_adjusted)));
    ceOutput.innerText = currentEfficiency.toFixed(1);
  }

  acidSlider.addEventListener('input', () => {
    acidVal.innerText = parseFloat(acidSlider.value).toFixed(2);
    calculateCE();
  });

  flowSlider.addEventListener('input', () => {
    flowVal.innerText = parseFloat(flowSlider.value).toFixed(1);
    calculateCE();
  });

  tempSlider.addEventListener('input', () => {
    tempVal.innerText = parseFloat(tempSlider.value).toFixed(1);
    calculateCE();
  });

  calculateCE();
</script>

The estimation assumes ideal ion behaviour despite the highly concentrated supporting electrolyte, a pore length of 500 \( \mu m\) (industrial benchmark for non-selective diaphragms), and a proton scaling ratio of 0.75 to account for its transport via both hopping and vehicular mechanisms. Other factors such as the structure (i.e., tortuosity and porosity) of the diaphragm and evolved gas bubbles can also impact the current efficiency.

## What do I do with all this acid and base?
The produced acid, along with a **reducing agent** such as hydrogen peroxide (H<sub>2</sub>O<sub>2</sub>), is used to dissolve the cathode active material while the base is used for **selective precipitation**. These precipitates are further processed into battery-grade precursors such as lithium carbonate (Li<sub>2</sub>CO<sub>3</sub>) and nickel-manganese-cobalt (NMC) hydroxides. The resulting salt from the precipitation step is **returned to the electrolyzer** for further acid-base production.

## References

[^1]: Baum et al. Lithium-Ion Battery Recycling—Overview of Techniques and Trends. *ACS Energy Lett.* **7**, 712−719 (2022). https://doi.org/10.1021/acsenergylett.1c02602
[^2]: Misleh et al. Li-ion battery recycling by energy-efficient, high-throughput Li<sub>2</sub>SO<sub>4</sub> salt splitting in a diaphragm flow cell. *Watt* **1**, 4 (2026). https://doi.org/10.1007/s44503-026-00003-3