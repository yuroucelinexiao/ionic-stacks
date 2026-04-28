---
title: "Why don't we just plant more trees?"
date: 2026-04-28
list_type: "dac"
draft: false
showWordCount: false
showTableOfContents: true
showHero: true
heroStyle: background
summary: "Investigating the land, time, and active intervention needed for reforestation."
categories: ["Direct Air Capture (DAC) Deep Dive"]
tags: ["CDR", "Trees", "Reforestation"]
---
{{< katex >}}

Limiting global warming to 1.5&deg;C requires removing 7–9 Gt<sub>CO2</sub>/year from the atmosphere by 2050[^1]. Currently, ~2 Gt<sub>CO2</sub>/year of carbon dioxide removal (CDR) is already happening, primarily through planting new trees. Amazing! So, if we only need to 4x our afforestation/reforestation efforts, why do we need tech-based CDR at all?

## All the land for all the trees
Outside of existing forests, agricultural, and urban land, Earth could potentially support an extra 0.9 billion hectares of continuous forest (almost the size of the United States)[^2]. Depending on the location and type of forest, an average 23 t<sub>CO2</sub>/ha/year could be removed during the first 20 years of tree growth[^3]. By that math, we could theoretically offset our entire CDR mandate for the next 46–59 years.

However, we must also consider how these lands are currently being used and the unintended side effects of mass afforestation, which can reduce the estimated CDR potential by a factor of 5[^4]:
- **Ecological displacement:** Some of this land consists of grasslands, savannas, and rangelands that already contain large carbon stores and support high levels of biodiversity[^5]. Researchers will need to investigate whether these ecosystems can sustain continuous forest growth and what impacts this transition would have on the net water and carbon balance.
- **The albedo effect:** Mature forests are lush and dark, lowering the Earth's surface albedo, especially in the Northern Hemisphere during snowy periods. This causes the surface to absorb more heat instead of reflecting it. The carbon capture benefits of new forests need to be balanced against their potential for increased heat absorption.

## Carbon removal over time
On average, a young, growing forest reaches its maximum CDR rate between 30 and 70 years[^6]. As trees mature, growth slows and the forest transitions from a carbon sink into a carbon reservoir.

While we must protect existing forests and plant new ones to increase our CDR capacity, we cannot rely on trees for our entire CDR mandate indefinitely—unless we develop the infrastructure to permanently sequester the carbon stored inside mature forests and reset the land for a new cycle of peak growth.

<div style="margin: 0 auto; text-align: center;">
{{<chart >}}
type: 'line',
data: {
  labels: ['', 'Young 🌱', '', 'Middle-aged', '', 'Mature 🌳', ''],
  datasets: [{
    data: [1,5,15,50,85,95,100],
    lineTension: 0.3,
    pointRadius: 0
  }]
},
options: {
  plugins: {
    legend: {
      display: false
    },
    title: {
      display: true,
      text: 'Carbon removal by forests versus age',
      font: {
        size: 16
      }
    }
  },
  scales: {
    x: {
      grid: {
        color: function(context) {
          return context.index % 2 === 0 ? 'rgba(128, 128, 128, 0.2)' : 'transparent';
        },
        drawTicks: false
      },
      ticks: {
        autoSkip: false,
        maxRotation: 0,
        minRotation: 0
      },
      title: {
        display: true,
        text: 'Forest age',
        font: {
          weight: 'bold'
        }
      }
    },
    y: {
      grid: {
        display: false
      },
      ticks: {
        display: false
      },
      title: {
        display: true,
        text: 'Total carbon removed',
        font: {
          weight: 'bold'
        }
      }
    }
  }
}
{{</chart >}}
</div>

## Active management of forests
Unmanaged forests are increasingly vulnerable to invasive species, pests, droughts, and wildfires[^7]. As forests decay or burn, CO<sub>2</sub> is released back into the atmosphere. To mitigate these risks, active forest management is required, including pest-control, removing excess biomass that fuels fires, sustainable harvesting/thinning, and controlled burns.

However, this level of intervention turns a natural ecosystem into a continuous industrial operation. The associated energy use and CO<sub>2</sub> emissions need to be accounted for when calculating the net efficiency of this CDR strategy.


## All CDR pathways are needed
The 7–9 Gt<sub>CO2</sub>/year CDR target is in addition to aggressive decarbonization across all sectors. Therefore, direct emission reduction remains the priority mitigation strategy. It is much easier to not release CO<sub>2</sub> in the first place than it is to pull it all back.

Alongside preserving existing forests and other natural carbon reservoirs, planting new forests is an effective way to remove significant amounts of CO<sub>2</sub> in the near term.

However, to achieve the annual CDR targets needed to limit global warming, we need to accelerate our collective removal capacity through tech-based pathways including biochar, biomass carbon removal and storage, enhanced weathering, ocean-based methods, and direct air capture. These engineered solutions can provide high-density, permanent sequestration to complement nature's limited carbon sink.

## References

[^1]: Smith, S. M. et al. (eds.) The State of Carbon Dioxide Removal 2024 - 2nd Edition. (2024). https://doi.org/10.17605/OSF.IO/F85QJ

[^2]: Bastin, J.-F. et al. The global tree restoration potential. Science 365, 76-79 (2019). https://doi.org/10.1126/science.aax0848

[^3]: Bernet, R. How Much CO2 Does A Tree Absorb? One Tree Planted (2023). https://onetreeplanted.org/blogs/stories/how-much-co2-does-tree-absorb

[^4]: Veldman, J. W. et al. Comment on "The global tree restoration potential". Science (2019). https://doi.org/10.1126/science.aay7976

[^5]: ILRI, IUCN, FAO, WWF, UNEP & ILC. Rangelands Atlas. Nairobi Kenya: ILRI (2021). https://hdl.handle.net/10568/114064

[^6]: Kelly, M. Managing Forests for Carbon, Resiliency, and Wildlife Habitat. Taking Action for Wildlife (2022). https://www.takingactionforwildlife.org/blog/2022/10/managing-forests-carbon-resiliency-wildlife-habitat

[^7]: Putney, J. D. et al. Introduction to Forest Carbon, Offsets and Markets. PNW 775 (2023). https://extension.oregonstate.edu/catalog/pnw-775-introduction-forest-carbon-offsets-markets
