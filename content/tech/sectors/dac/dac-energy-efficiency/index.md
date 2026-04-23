---
title: "How much energy do we actually need to pull CO<sub>2</sub> out of thin air?"
date: 2024-04-06
list_type: "dac"
draft: false
showWordCount: false
showTableOfContents: true
showHero: true
heroStyle: background
summary: "Technical foundations on minimum work, actual work, and second law efficiencies for direct air capture."
categories: ["Direct Air Capture (DAC) Deep Dive"]
tags: ["eDAC", "Energy-Efficiency", "First-Principles", "Second Law", "Thermodynamics", "Regeneration"]
---
{{< katex >}}

## The minimum theoretical work

There's nothing engineers love more than energy-efficient systems. In a perfect system, 100% of the energy input performs useful work. When it comes to direct air capture, useful work means gathering dispersed CO<sub>2</sub> molecules from the air into a concentrated gas stream. This process decreases entropy and is non-spontaneous. Thus, there is a thermodynamic minimum work of separation (\(W_{ \text{min}}\)), the absolute energy floor for a reversible, 100% efficient process.

To calculate \(W_{ \text{min}}\), we turn to the Gibbs free energy of mixing (\( \Delta G_{ \text{mix}}\)). We assume constant temperature and pressure, and treat air as an ideal gas where the enthalpy of mixing is zero (\(\Delta H_{ \text{mix}}=0\)). Gibbs free energy is derived from the First and Second Laws of Thermodynamics and represents the work needed to overcome the tendency of molecules to disperse and mix (some statistical mechanics required).

<div style="margin: 0 auto; text-align: center;">
\(W_{ \text{min}}=- \Delta G_{ \text{mix}}=-nRT \sum x_i \ln(x_i)\)
</div>

Where:
- \(n\) is the number of moles
- \(R\) is the universal ideal gas constant (\(8.314 \, \text{J}/( \text{mol} \cdot \text{K})\))
- \(T\) is the temperature (\(298.15 \text{ K}\))
- \(x_i\) is the mole fraction of gas \(i\) (\(x_1\) is \(\text{CO}_2\) and \(x_2\) is everything else)

Note the negative sign here! \(\Delta G_{ \text{mix}}\) itself is negative because mixing is a spontaneous process, and \(W_{ \text{min}}\) will be positive because we have to put in work. Sprinkle in some algebra to normalize the equation for 1 mole of \(\text{CO}_2\). The negative sign then cancels out due to a log identity. The equation becomes:

<div style="margin: 0 auto; text-align: center;">
\(W_{ \text{min}}=RT \left[ \ln \left( \dfrac{1}{x_ \text{in}} \right)+ \dfrac{1-{x_ \text{in}}}{x_ \text{in}} \ln \left( \dfrac{1}{1-{x_ \text{in}}} \right) \right]\)
</div>

Where:
- \(x_ \text{in}\) is the concentration of \(\text{CO}_2\) flowing into the system (\(425 \text{ ppm}\))

This equation can be further simplified since \(x_ \text{in}\) is very small:

<div style="margin: 0 auto; text-align: center;">
\(W_{ \text{min}} \approx RT \left[ \ln \left( \dfrac{1}{x_ \text{in}} \right)+ 1 \right]\)
</div>

When we plug in our ambient conditions, we find the minimum required energy for direct air capture, before a single fan, pump, heater, or power supply has been turned on:

<div style="margin: 0 auto; text-align: center;">
\(W_{ \text{min}} \approx \mathbf{21.7 \, \text{kJ/mol}} \approx \mathbf{0.49 \, \text{GJ/t}_{\text{CO}_2}} \approx \mathbf{137 \, \text{kWh/t}_{\text{CO}_2}}\)
</div>

## Real systems are hard
Real systems involve irreversibilities (e.g. fluid friction, thermal gradients, and kinetic overpotentials) that increase the actual energy requirement. Let's take [Carbon Engineering](https://www.carbonengineering.com)'s direct air capture using an aqueous potassium hydroxide sorbent as an example. Their pilot plant data was published in 2018[^1].

**The first challenge: moving massive volumes of air through a sorbent interface.**

CO<sub>2</sub> is very dilute in the atmosphere and capturing 1 tonne of CO<sub>2</sub> requires processing ~2.62 million m<sup>3</sup> of air (\(V_{ \text{air}}\)), assuming a 50% capture efficiency. These CO<sub>2</sub> capture units, or air contactors, use structured packing with high surface-area-to-volume ratios to maximize the reaction interface. Imagine, perhaps, a tightly layered corrugated cardboard structure.

High-powered fans are needed to overcome the pressure drop (\( \Delta P\)) and push the air through. The specific fan energy (\(E_{\text{fan}}\)) can be calculated using the following equation, assuming a \( \Delta P\) of 100 Pa and fan efficiency (\(\eta_{\text{fan}}\)) of 70%:

<div style="margin: 0 auto; text-align: center;">
\(E_{\text{fan}} = \dfrac{V_{ \text{air}} \Delta P}{ \eta_{\text{fan}}}\)
</div>

The capture efficiency and \( \Delta P\) assumptions are slightly more conservative than the reported numbers. Nevertheless, they provide a reasonable baseline for an average air contactor:

<div style="margin: 0 auto; text-align: center;">
\(E_{\text{fan}} \approx \mathbf{0.37 \, \text{GJ/t}_{\text{CO}_2}} \approx \mathbf{104 \, \text{kWh/t}_{\text{CO}_2}}\)
</div>

**The second (perhaps much more daunting) challenge: separating CO<sub>2</sub> from the sorbent.**

Sorbent selection is sticky business. A delicate balance needs to be achieved: strong-binding sorbents have fast reaction kinetics and can efficiently remove CO<sub>2</sub> from air, but if the binding is too strong, massive amounts of energy are required to release it. Conventional thermal-swing processes use high-grade heat to break these chemical bonds and regenerate the sorbent. In  real systems, the applied heat is much more than the theoretical energy of the bond because it has to account for heating up the CO<sub>2</sub> and everything around it, while overcoming the activation energy barrier.

In the Carbon Engineering process, a precipitation step was added after the air contactor to reduce the energy wasted on water evaporation. Even so, a good chunk of thermal energy was used for sorbent regeneration at 900&deg;C:

<div style="margin: 0 auto; text-align: center;">
\(E_{\text{regen}} \approx \mathbf{5.25 \, \text{GJ/t}_{\text{CO}_2}} \approx \mathbf{1458 \, \text{kWh/t}_{\text{CO}_2}}\)
</div>

**Minor loads still add up**

Beyond the main fans and sorbent regenerator, the plant also needs energy for supporting equipment. These can include fluid pumps, CO<sub>2</sub> compressors, air separation units, and auxiliary equipment.

## Just here for the table (TLDR)

The total energy needed to pull CO<sub>2</sub> out of thin air varies significantly across the industry, driven by 3 key factors:
- **Capture chemistry:** liquid absorption, solid adsorption, or physisorption
- **Sorbent type:** alkali hydroxides, amine-functionalized solids, or porous membranes
- **Regeneration mode:** thermal or electrochemical

Below is a summary of the energy consumption reported by select companies, adapted from Wang et al[^2].

<div style="width: fit-content; margin: 0 auto;">

| Company | Technology | <div style="width: 200px;">Total energy consumption</div> (\(\text{GJ/t}_{\text{CO}_2}\)) / (\(\text{kWh/t}_{\text{CO}_2}\)) | <div style="width: 70px;">Energy efficiency (\%\)</div> |
|:---:|:---:|:---:|:---:|
| [Carbon Engineering](https://www.carbonengineering.com) | Thermal-swing absorption | 6.3–7.2 / 1,750–2,000 | 7–8% |
| [Climeworks](https://www.climeworks.com) | Temperature-vacuum swing adsorption | 6.3–7.2 / 1,750–2,000 | 7–8% |
| [Mission Zero](https://www.missionzero.tech) | pH-swing absorption | 1.4–2.3 / 400–650 | 21–34% |

</div>

## Electrochemical direct air capture

While there are many ways to reduce energy consumption, one way forward is turning to electrochemistry. These systems use different sorbent regeneration mechanisms that more precisely target the CO<sub>2</sub>-sorbent bond, eliminating the bulk-heating requirements of conventional processes entirely.

As the global energy landscape evolves, the industrial deployment of direct air capture must align with the availability of excess renewable electricity. Electrochemical systems are fully electrified and can be strategically installed in remote regions with ample renewable capacity. Modular and flexible, they are a strong contender for scalable and sustainable carbon removal technology.

## References

[^1]: Keith, H., Holmes, G., St. Angelo, D. & Heidel, K. A process for capturing CO<sub>2</sub>‚ from the atmosphere. Joule 2, 1573-1594 (2018). https://doi.org/10.1016/j.joule.2018.05.006

[^2]: Wang, E. et al. Reviewing direct air capture startups and emerging technologies. Cell Rep. Phys. Sci. 5, 101791 (2024). https://doi.org/10.1016/j.xcrp.2024.101791
