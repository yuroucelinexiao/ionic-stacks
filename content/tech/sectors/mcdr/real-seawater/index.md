---
title: "When electrochemistry meets the open seas | Ionic Stacks"
date: 2026-04-11
list_type: "mcdr"
draft: false
showWordCount: false
showTableOfContents: true
showHero: true
heroStyle: background
summary: "everything hard about seawater"
categories: ["Marine Carbon Dioxide Removal (mCDR) Deep Dive"]
tags: ["ocean", "seawater"]
---
{{< katex >}}

## Seawater composition
Synthetic seawater is a great laboratory tool for studying marine-based technologies. However, the ocean is a living electrolyte, and not so forgiving. Even after we take out the fish, seaweed, and sand, we are still left with a complex mix of ions. The table below summarizes the major constituents of seawater, adapted from Sverdrup and Armbrust[^1]:

<div style="width: fit-content; margin: 0 auto;">

| <div style="width: 175px;">Component</div> | <div style="width: 175x;"> Approx. Concentration (mM)</div> |
| :---: | :---: |
| Chloride (Cl<sup>-</sup>) | ~560 |
| Sodium (Na<sup>+</sup>) | ~481 |
| Magnesium (Mg<sup>2+</sup>) | ~54 |
| Sulfate (SO<sub>4</sub><sup>2-</sup>) | ~29 |
| Calcium (Ca<sup>2+</sup>) | ~11 |
| Potassium (K<sup>+</sup>) | ~10 |
| Bicarbonate (HCO<sub>3</sub><sup>-</sup>) | ~2 |

</div>

## Only ~2 mM of DIC
**Challenge:** From the [chemical inventory](#seawater-composition) above, we can immediately see the primary bottleneck of mCDR: the dilute concentration of DIC (primarily in the form of bicarbonate). In an ideal system, ~11,360 tonnes of seawater needs to be processed to extract 1 tonne of CO<sub>2</sub>. In real systems, the volume of water required increases based on the target pH of the electrochemical stack (which determines CO<sub>2</sub> speciation based on the Henderson-Hasselbalch equation), and the time allowed for CO<sub>2</sub> degassing (which is governed by Fick's Law of Diffusion and two-film boundary layer equations). The electrical energy required for the intake pumps can quickly add up if large volumes of water need to be pumped over a steep pressure drop (\(\Delta P\)).

Try the slider below to contextualize how much water we would have to process to extract 1 tonne of CO<sub>2</sub>. The estimation assumes a composite acid dissociation constant (\(pK_a\)) of 5.84[^2], which considers the dehydration of carbonic acid and seawater salinity, and a volumetric mass transfer coefficient (\(k_La\)) of 0.045 s<sup>-1</sup>, which is representative of an optimized industrial-scale degasser.

<div style="background: #0B3A46; padding: 25px; border-radius: 12px; border: 1px solid #A6A6A6; color: white; font-family: sans-serif; max-width: 700px; margin: 0 auto;">
  
  <h3 style="margin-top: 0; color: #B89C3F;">Seawater needed per tonne CO<sub>2</sub></h3>

  <label>Electrochemical stack target pH: <strong id="ph-val">5.0</strong> (max extractable CO<sub>2</sub>: <strong id="theo-yield">87</strong>%)</label>
  <input type="range" id="ph-slider" min="4.0" max="8.1" step="0.1" value="5.0" style="width: 100%; margin-top: 20px; accent-color: #B89C3F;">

  <label>CO<sub>2</sub> degassing time: <strong id="time-val">30</strong> s (actual CO<sub>2</sub> yield: <strong id="actual-yield">65</strong>%) </label>
  <input type="range" id="time-slider" min="1" max="120" value="30" style="width: 100%; margin-top: 20px; accent-color: #B89C3F;">

  <div style="background: white; padding: 15px; border-radius: 8px; text-align: center; margin-top: 20px;">
    <span style="font-size: 16px; color: grey; text-transform: uppercase; letter-spacing: 1px;">Seawater Processed</span><br>
    <span id="water-output" style="font-size: 36px; font-weight: bold; color: #B89C3F;">17,557</span>
    <span style="color: #B89C3F;"> tonnes</span><br>
    <span id="volume-analogy" style="font-size: 16px; color: grey; font-style: italic; display: inline-block;">(~7 Olympic swimming pools)</span>
  </div>
</div>

<script>
  const phSlider = document.getElementById('ph-slider');
  const timeSlider = document.getElementById('time-slider');
  const phVal = document.getElementById('ph-val');
  const timeVal = document.getElementById('time-val');
  const theoYieldText = document.getElementById('theo-yield');
  const actualYieldText = document.getElementById('actual-yield');
  const waterOutput = document.getElementById('water-output');
  const analogyOutput = document.getElementById('volume-analogy');

  const min_water = 11363; 
  const pKa = 5.84; {{/* composite pKa for seawater*/}}
  const k_La = 0.045; {{/* volumetric mass transfer coefficient (k_La) ranges between 0.01 to 0.1 s^(-1) */}}

  function getVolumeAnalogy(tonnes) {
    if (tonnes >= 10000000) {
      return "(Small inland lake)";
    } else if (tonnes >= 1000000) {
      let stadiums = Math.round(tonnes / 1000000);
      return `(~${stadiums} flooded stadium(s))`;
    } else if (tonnes >= 250000) {
      let minutes = Math.round(tonnes / 144000);
      return `(~${minutes} minute(s) of continuous flow over Niagara Falls)`;
    } else {
      let pools = Math.round(tonnes / 2500);
      return `(~${pools} Olympic swimming pools)`;
    }
  }

  function calculateThermodynamics() {
    let current_pH = parseFloat(phSlider.value);
    let contactTime = parseFloat(timeSlider.value);

    let theoreticalYield = 1 / (1 + Math.pow(10, current_pH - pKa));
    let actualYield = theoreticalYield * (1 - Math.exp(-k_La * contactTime));

    let safeYield = Math.max(actualYield, 0.0001); 
    let requiredWater = min_water / safeYield;

    theoYieldText.innerText = (theoreticalYield * 100).toFixed(0);
    actualYieldText.innerText = (actualYield * 100).toFixed(0);
    
    let displayWater = requiredWater > 9999999 ? "> 9,999,999" : requiredWater.toLocaleString(undefined, { maximumFractionDigits: 0 });
    waterOutput.innerText = displayWater;

    analogyOutput.innerText = getVolumeAnalogy(requiredWater);
  }

  phSlider.addEventListener('input', () => {
    phVal.innerText = parseFloat(phSlider.value).toFixed(1);
    calculateThermodynamics();
  });

  timeSlider.addEventListener('input', () => {
    timeVal.innerText = timeSlider.value;
    calculateThermodynamics();
  });

  calculateThermodynamics();
</script>

**Solution:** To reduce the energy requirement of intake pumps, mCDR systems can minimize the (\(\Delta P\)) through wide, shallow, open-channel flow designs. The electrochemical stack can also be suspended in a flowing water stream, leveraging the power of gravitational and tidal forces for passive pumping. Although this design entirely eliminates the mechanical pumps, it introduces variability in the flow rate and stricter material requirements.

## Microbes and particulates
**Challenge:** Electrolyzers are notoriously sensitive to solid matter. Microorganisms and suspended particulates will not only clog narrow electrolyte flow channels, but also foul the membranes and electrodes, rapidly degrading stack performance. The immediate engineering response is, of course, filtration. However, the pumping energy scales directly with the volume of water processed and the pressure drop of the filters required to achieve high purity.

**Solution:** Fortunately, many existing coastal facilities already have high water purification standards. By integrating mCDR stacks directly downstream of desalination plants or once-through power plant cooling systems, the pumping and filtration costs are significantly reduced. Alternatively, the stack design can be made robust enough to survive the biological load through periodic cleaning. This includes hydraulic backwashing and periodic polarity reversal (PPR) which dissolves organic matter through localized pH swings. However, this approach sacrifices total system uptime and increase hardware complexity.

## Chlorine evolution

**Challenge:** Going back to the [seawater composition](#seawater-composition) table again, we see that Cl<sup>-</sup> is the number 1 ion floating in the ocean. On the anode, Cl<sup>-</sup> can oxidize and evolve into toxic chlorine gas (Cl<sub>2</sub>) or bleach (ClO<sup>-</sup>), posing a threat to both the long-term operation of the electrochemical stack and the marine ecosystem. The chlorine evolution reaction (ClER) diverts anodic current away from the target reaction, which is to produce protons and generate an acidic stream for either CO<sub>2</sub> extraction or valorization, reducing the energy efficiency of the overall process.

**Solution:** Chlorine generation can be suppressed by altering the reaction kinetics and thermodynamics at the anode, restricting the local mass transfer of Cl<sup>-</sup> at the boundary layer, or flowing seawater in separate compartments to physically isolate the anode[^3].
- **Kinetics and thermodynamics:** The thermodynamic potential for ClER is close to the target proton-producing oxygen evolution reaction (OER):

  \( \text{OER:} \quad H_2O \rightarrow \frac{1}{2} O_2 + 2H^+ + 2e^- (E^ \circ = 1.23 \, \text{V vs. SHE})\)

  \( \text{ClER:} \quad 2Cl^- \rightarrow Cl_2 + 2e^- (E^ \circ = 1.36 \, \text{V vs. SHE})\)

  We can simultaneously lower the activation energy for OER and increase the kinetics barrier for ClER by designing selective catalysts. Increasing the local anode pH can further promote OER over ClER. Alternatively, we can switch to anode reactions that are thermodynamically more favourable, constraining  the anodic potential to prevent chlorine evolution. One example is the hydrogen oxidation reaction (HOR), which can proceed at a much lower voltage but introduces complexities in gas handling and material selection:

  \( \text{HOR:} \quad H_2 \rightarrow 2H^+ + 2e^- (E^ \circ = 0.00 \, \text{V vs. SHE})\)

- **Mass transfer:** This approach focuses on keeping the Cl<sup>-</sup> away from the anode by altering the local reaction environment. Coatings and adlayers can act as molecular sieves that use steric hindrance and electrostatic repulsion to reduce Cl<sup>-</sup> concentration at the active sites.
- **Stack design:** Sometimes an architectural overhaul is exactly what we need. Instead of feeding seawater to the anode compartment, we can use membranes to create physical barriers and confine the seawater to central flow channels. One example of this is the bipolar membrane electrodialysis stack. This approach achieves near-complete Cl<sup>-</sup> isolation (dependent on the permselectivity of the membranes) but also increases the stack's ohmic resistance.

## Magnesium and calcium precipitates

**Challenge:** Going back to the [seawater composition](#seawater-composition) table one last time, we see that Mg<sup>2+</sup> and Ca<sup>2+</sup> also exist in significant quantities. As the cathode generates OH<sup>-</sup> to produce the target alkaline stream, the localized high-pH environment precipitates Mg<sup>2+</sup> as Mg(OH)<sub>2</sub> and shifts the bicarbonate equilibrium to precipitate Ca<sup>2+</sup> as CaCO<sub>3</sub>. These precipitates passivate the catalyst, clog the flow channels, and rupture the ion-exchange membranes.

**Solution:** Similar to the fight against chlorine generation, seawater can be confined to central flow channels to keep Mg<sup>2+</sup> and Ca<sup>2+</sup> away from the cathode's localized alkaline environment. An alternative, operationally driven, head-on approach continuously removes the mineral scale through frequent polarity reversals, periodic solubility shifts, and raw hydrodynamic forces.

## References

[^1]: Sverdrup, K. A. & Armbrust, E. V. *An Introduction to the World's Oceans* 10th edn (McGraw-Hill, 2008).

[^2]: Millero, F. J., Graham, T. B., Huang, F., Bustos-Serrano, H. & Pierrot, D. Dissociation constants of carbonic acid in seawater as a function of salinity and temperature. *Mar. Chem.* **100**, 80-94 (2006). https://doi.org/10.1016/j.marchem.2005.12.001

[^3]: Bahuguna, G. & Patolsky, F. Routes to Avoiding Chlorine Evolution in Seawater Electrolysis: Recent Perspective and Future Directions. *ACS Materials Lett.* **6**, 3202-3217 (2024). https://doi.org/10.1021/acsmaterialslett.4c00409