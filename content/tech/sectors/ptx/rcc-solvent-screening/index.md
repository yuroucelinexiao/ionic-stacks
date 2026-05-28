---
title: "Solvent lead generation for stable RCC electrolysis"
date: 2026-05-15
list_type: "ptx"
draft: false
showWordCount: false
showTableOfContents: true
showHero: true
heroStyle: background
summary: "RCC solvent screening using RDKit and regression models"
categories: ["Power-to-X (PtX) Deep Dive"]
tags: ["Reactive capture of CO2", "RCC", "Solvent", "Descriptors", "QSAR", "Linear regression", "Screening", "Lead generator", "DOE"]
---
{{< katex >}}

<style>
  table th, table td {
    vertical-align: middle !important;
  }
</style>

## Solvents in RCC systems

Reactive CO<sub>2</sub> capture (RCC) directly uses CO<sub>2</sub>-rich post-capture solutions as reactor feedstocks, eliminating the conventional thermal regeneration step and simplifying the overall process. However, a major challenge for electrochemical RCC is the **electrolysis stability**.

[Xiao et al.](/tech/#23-solvent-tuning-regulates-proton-flux-to-extend-stability-in-reactive-co2-capture-and-electrolysis) recently found that **solvent tuning can extend stability** by regulating the cathode local pH[^1]. Initially, 5 amino-acid-salt capture solvents were tested and potassium glycinate (K-GLY) exhibited the longest stability. Glycine, with its **relatively small size and moderate acid dissociation constant (pK<sub>a</sub>) values**, may interact less with the catalyst, leading to higher CO<sub>2</sub> conversion efficiency and longer stability.

<div style="width: fit-content; margin: 0 auto;">

| <div style="width: 100px;">Solvent</div> | <div style="width: 125px;">Stability (hours)</div> | <div style="width: 150px;">Highest basic pK<sub>a</sub></div> |
|:---:|:---:|:---:|
| K-GLY | 13 | 9.60 |
| K-LYS | 1 | 10.79 |
| K-PRO | 2 | 10.60 |
| K-SER | 3 | 9.15 |
| K-SAR | 5 | 10.35 |

</div>

K-GLY is a good RCC solvent, but there are probably better ones out there. The question is: how do we find the best RCC solvents without testing every single formulation?

## Let cheminformatics and stats do some heavy lifting

Using the initial experimental data set (n = 5), we can do some simple analysis. With a small sample size, it's easy to overfit the data, draw false conclusions from extrapolations, and find spurious correlations. Therefore, this will be a **leads generation** exercise that can serve as a starting point for future experiments.

This is the workflow:
1. Use [RDKit](https://www.rdkit.org/), an open-source cheminformatics software, to extract over 200 physical and chemical properties (descriptors) of each amino acid.
2. Calculate the Pearson correlation (i.e., linear relationship) between every descriptor and stability.
3. Find the descriptors with the highest correlation and use these properties to screen solvent candidates.
4. Use pK<sub>a</sub> as a filter to evaluate the shortlisted candidates.

[Download code, experimental dataset, and screening libraries](ionic-stacks-rcc-solvent-screening.zip) {{< icon "download" >}}

## Top descriptors

These are the top 5 descriptors that correlated with stability:

<div style="width: fit-content; margin: 0 auto;">

| <div style="width: 150px;">Descriptor</div> | <div style="width: 100px;">Correlation (r)</div> | <div style="width: 300px;">Characteristics for longer stability</div> |
|:---:|:---:|:---:|
| BCUT2D_CHGLO | 0.95 | Less nucleophilic groups |
| FractionCSP3 | -0.93 | Lower fraction of sp<sup>3</sup> hybridized carbons |
| BCUT2D_LOGPLOW | 0.88 | More hydrophobic |
| MaxAbsEStateIndex | -0.87 | Less locally polarized groups |
| BertzCT | -0.84 | Simpler structure |

</div>

Xiao et al. observed a small increase in series resistance (R<sub>s</sub>) and a large increase in charge transfer resistance (R<sub>ct</sub>) post-electrolysis, suggesting that performance loss is dominated by **degradation processes localized at the catalytic interface**.

Among the top 5 descriptors, **BCUT2D_CHGLO** and **BertzCT** align well with the proposed degradation mechanisms. Highly nucleophilic solvents (tracked by the **global electronic** descriptor BCUT2D_CHGLO) reduce local CO<sub>2</sub> availability and interact with the catalyst. Larger, more complex solvents (tracked by the **topological** descriptor BertzCT) increase viscosity and hinder mass transport, potentially blocking catalytically active sites.

Given the limited degrees of freedom and their high collinearity (r≈-0.95), modeling these two descriptors together would lead to overfitting and redundancy. However, because **each descriptor tracks distinct solvent properties**, we will build separate linear regression models for each one and include both in the screening process.

{{<gallery>}}

  {{<figure
    src="stability_vs_BCUT2D_CHGLO.png"
    alt="Stability vs. BCUT2D_CHGLO"
    target="_self"
    figureClass="grid-w100 lg:grid-w50" >}}

  {{<figure
    src="stability_vs_BertzCT.png"
    alt="Stability vs. BertzCT"
    target="_self"
    figureClass="grid-w100 lg:grid-w50" >}}

{{</gallery>}}

The shaded region represents the 95% confidence interval.

## pK<sub>a</sub>

Amino acids with higher amino-group pK<sub>a</sub> values are more nucleophilic, whereas those with lower pK<sub>a</sub> values can enhance hydrogen evolution by direct proton donation. While a **quadratic fit** was used to model the relationship between pK<sub>a</sub> and stability, the **small sample size meant that the model was not statistically significant** (n = 5, F(2, 2) = 3.13, p = 0.24). Despite the visual trend, more data is required to determine a reliable optimum. Therefore, an empirical range (9.15–10.35) defined by the three solvents with the highest stability was used to filter leads for the solvent screening.

<div style="display: flex; justify-content: center;">

{{<figure
    src="stability_vs_pka.png"
    alt="Stability vs. pKa"
    target="_self"
    figureClass="grid-w75" >}}

</div>

## Screening 21 amino acids

The linear regression models, trained on the experimental dataset, were used to screen a library of 21 amino acids to identify alternative solvent candidates. Stability was predicted using independent, single-descriptor models for BCUT2D_CHGLO and BertzCT. Candidates that ranked in the top 10 of both models were then ranked by their average predicted stability. Among the 21 amino acids, **glycine** and **sarcosine** ranked highest, while **alanine** emerged as a promising additional candidate.

<div style="width: fit-content; margin: 0 auto;">

| <div style="width: 130px;">Amino Acid</div> | <div style="width: 100px;">Predicted<br/>stability<br/>BCUT2D_CHGLO<br/>(hours)</div> |  <div style="width: 75px;">Predicted<br/>stability<br/>BertzCT<br/>(hours)</div> | <div style="width: 75px;">Average<br/>predicted<br/>stability<br/>(hours)</div> | <div style="width: 65px;">Highest basic pK<sub>a</sub></div> |
|:---:|:---:| :---:|:---:| :---: |
| Glycine | 11.5 | 9.5 | 10.5 | 9.60 |
| Sarcosine | 7.5 | 8.0 | 7.7 | 10.35 |
| Alanine | 5.2 | 6.9 | 6.1 | 9.69 |

</div>

## Screening 167 capture solvents

Using the same methodology, the screening was then expanded to a larger library of 167 carbon capture solvents from literature[^2].

<div style="width: fit-content; margin: 0 auto;">

| <div style="width: 130px;">Solvent</div> | <div style="width: 100px;">Predicted<br/>stability<br/>BCUT2D_CHGLO<br/>(hours)</div> |  <div style="width: 75px;">Predicted<br/>stability<br/>BertzCT<br/>(hours)</div> | <div style="width: 75px;">Average<br/>predicted<br/>stability<br/>(hours)</div> | <div style="width: 65px;">Highest basic pK<sub>a</sub></div> |
|:---:|:---:| :---:|:---:| :---: |
| Ethylamine | 18.8 | 15.5 | 17.1 | 10.87 |
| Propylamine | 12.5 | 15.1 | 13.8 | 10.71 |
| Monoethanolamine (MEA) | 12.2 | 14.7 | 13.4 | 9.50 |
| Ethylenediamine (EDA) | 11.85 | 15.0 | 13.4 | 9.92 |
| Butylamine | 8.83 | 14.2 | 11.53 | 10.78 |
| 1,3-diaminopropane </br> (1,3-DAP) | 8.5 | 14.0 | 11.3 | 10.62 |
| 3-amino-1-propanol </br> (3-AP) | 8.8 | 13.7 | 11.3 | 9.96 |

</div>

4 of the top 7 candidates (ethylamine, propylamine, butylamine, and 1,3-DAP) had max pK<sub>a</sub> values above the previously determined optimal range. They are also volatile and not suitable for industrial CO<sub>2</sub> capture.

This lead generation exercise found **MEA**, **EDA**, and **3-AP** as the most promising solvent candidates for further evaluation.

## Better data = better model = save money

To improve the accuracy and reliability of this model, we need more high-quality data.

- **Sample size constraints:** The current training dataset has only 5 points—a statistical nightmare for achieving high-confidence results. Expanding the dataset will allow for simultaneous multivariable models that better capture the complex solvent chemistry.
- **Design of experiments (DOE):** The next sets of experiments should target the limits and boundaries of the top descriptors. This will provide the variance needed to reduce sample collinearity.
- **Applicability domain:** The model was trained on only amino acid salts and should not be directly extrapolated to predict other solvent classes. Including a wider range of solvents in the next set of experiments would make the model more robust.

A suitable solvent for the integrated system needs to be both a **good capture agent** and a **good electrolyte**. Transport and electrochemical properties, including conductivity, viscosity, electrochemical stability, and catalyst interactions, are not typically considered in conventional carbon capture. With so many competing variables at play, an **experimentally-informed model** provides a starting point that can drastically reduce the time and cost of laboratory screening.

## References

[^1]: Xiao et al. Solvent tuning regulates proton flux to extend stability in reactive CO<sub>2</sub> capture and electrolysis. *Chem Catalysis* **6**, 101694 (2026). https://doi.org/10.1016/j.checat.2026.101694

[^2]: McDonagh, J. L. et al. Chemical space analysis and property prediction for carbon capture solvent molecules. *Digital Discovery* **3**, 528-543 (2024). https://pubs.rsc.org/en/content/articlehtml/2024/dd/d3dd00073g