<h1 align="center">Hi, I'm Harris 👋</h1>

<p align="center">
  <b>Chemical engineer turned production engineer.</b><br>
  I build tools that make production systems easier to understand, simulate and improve.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/MSc-KTH%20Royal%20Institute%20of%20Technology-004791?style=flat-square" alt="KTH">
  <img src="https://img.shields.io/badge/BSc-Cyprus%20University%20of%20Technology-555?style=flat-square" alt="CUT">

</p>

<p align="center">
  <a href="https://www.linkedin.com/in/charilaos-p-stavrou-648a25249">LinkedIn</a>
</p>

---

## Production Engineering Toolkit

Four tools, one story: from formulas to simulation. Each has a live demo, tests, and a README that states its formulas, assumptions and limitations.

| Tool | What it does | Highlight |
|---|---|---|
| **[Production Line Simulator](https://github.com/CharilaosStavrou/line-simulatorv1)** ([live demo](https://line-simulatorv1.vercel.app)) | Discrete-event simulation of a serial line with breakdowns, finite buffers and blocking, animated, with 95% confidence intervals | Engine written from scratch, **98 tests**, validated against M/M/1 theory and Little's law |
| **[VSM Tool](https://github.com/CharilaosStavrou/vsm-tool)** ([live demo](https://vsm-tool-five.vercel.app)) | Build a Value Stream Map and get takt time, lead time, PCE and bottleneck automatically | Exports PNG / JSON, formulas shown next to every metric |
| **[Kanban Calculator](https://github.com/CharilaosStavrou/kanban-calculator)** | Size kanban loops and supermarkets | Companion to the VSM tool |
| **[Aggregate Planning](https://github.com/CharilaosStavrou/aggregate-planning)** | Compares Chase, Level and Mixed strategies against an LP-optimal plan | Heuristics vs optimum, side by side |

### A result I like

In the simulator's sample line, raising **one** buffer in front of an unreliable welding station from 2 to 20 parts:

- throughput **+22%**
- bottleneck moves from Welding to Machining
- but WIP grows **2.7×** and cycle time **2.2×**

More output is bought with more inventory and longer lead time, and the root cause (long repairs) is still there. This is the kind of trade-off I want to study in real plants.

## Beyond software

- **ELVAL (aluminium manufacturing)**: Chemical Engineering Intern on coil coating line monitoring (2025); seasonal assistant (2024)
- **University of Milan**: research internship on supported metal catalysts for hydrogen generation and photocatalysis (2025)
- **BSc thesis**: photocatalytic hydrogen production in a microreactor, combining experiments with COMSOL Multiphysics simulation
- **Youth Parliament of Cyprus**: member of the Environmental Committee (policy discussions, youth advocacy)

## Skills

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![MATLAB](https://img.shields.io/badge/MATLAB-0076A8?style=flat-square)
![COMSOL](https://img.shields.io/badge/COMSOL-Multiphysics-5C7CFA?style=flat-square)
![Excel](https://img.shields.io/badge/Excel-217346?style=flat-square&logo=microsoftexcel&logoColor=white)

**Topics I work with:** discrete-event simulation · lean / value stream mapping · production planning · queueing theory · process modelling · photocatalysis and reactor simulation

## Let's talk

If something here caught your eye, or you just want to talk shop, I'd love to hear from you.<br><br> <a href="https://www.linkedin.com/in/charilaos-p-stavrou-648a25249"><b>Connect with me on LinkedIn →</b></a> </p>

# Photocatalytic hydrogen from hydrous hydrazine: experiments and a coupled CFD model

**BSc thesis · Chemical Engineering · Cyprus University of Technology · May 2026**
Supervisor: Prof. Achilleas Konstantinou. Experimental work at the Department of Industrial Chemistry, University of Milan (Prof. Alberto Villa).

*Full title: Experimental and Computational Investigation of Photocatalytic Hydrous Hydrazine Decomposition for Hydrogen Production over Rh-Based Catalysts in Stirred Batch Photoreactors.*

## In short

I made a Rh/TiO₂ photocatalyst, tested it in two stirred batch photoreactors, and set up a 2D COMSOL model that couples turbulent flow, UV radiation transport and reaction kinetics. The model shows where in each reactor the reaction happens. A parametric study shows that more lamp power stops helping at the irradiance used in the experiments.

## Key numbers

| What | Result |
|---|---|
| Catalyst screening (dark, 18 mL reactor) | 0.5% Rh/TiO₂-P25 reached 1.072 bar peak pressure, about 6× the next best catalyst (1% Cu/TiO₂, 0.167 bar) |
| Effect of UV on Rh/TiO₂-NiO | 1.798 bar in the dark, 2.095 bar under UV (+17%) |
| 150 mL photoreactor, 120 min, UV | 73.6% hydrazine conversion, 127 mL of gas (H₂ + N₂) collected |
| Irradiance sweep (model) | The minimum hydrazine concentration stops falling at the experimental irradiance: 2.98 M at both 13,918 and 15,000 W m⁻² sr⁻¹ |

## Why this problem

Hydrous hydrazine (N₂H₄·H₂O) holds a lot of hydrogen and produces no carbon-containing products, so it is studied as a chemical hydrogen carrier. Rh on TiO₂ is very active, and UV light can add a photocatalytic contribution on top of the thermal one.

In a stirred photoreactor, three things decide performance together: how the flow distributes the catalyst, how far light penetrates the suspension, and the reaction kinetics. The literature review in the thesis found no model that combined all three for hydrazine decomposition over Rh/TiO₂-P25 in a stirred batch reactor, so that is what I set out to build.

## Experiments

- **Catalyst:** 0.5 wt% Rh on TiO₂-P25 by wet impregnation (RhCl₃), dried at 80 °C, then reduced in H₂ at 400 °C.
- **Reactor 1, 18 mL sealed flask:** magnetic stirrer at 1400 RPM, 150 µL of 3.3 M hydrous hydrazine in 5 mL water. Gas evolution from the headspace pressure (ideal gas law). Dark runs in a heated oil bath, UV runs with an external lamp.
- **Reactor 2, 150 mL cylindrical photoreactor:** UV lamp submerged on the axis, water-cooled. Hydrazine followed every 30 min by UV-vis (DMAB colorimetric method), total gas volume by water displacement.
- **Screening:** four catalysts, three TiO₂ phases (anatase, rutile, P25), stirring rate (250 to 1000 RPM) and catalyst loading (1:8 to 1:40).

## Model

A 2D cross-section of each reactor in COMSOL Multiphysics 5.5, with three physics solved in sequence:

1. **Flow:** k-ε RANS turbulence with the frozen-rotor approach for the stirrer. Gives the velocity field and turbulent viscosity.
2. **Radiation:** P1 approximation in participating media. Gives the local volumetric rate of photon absorption (LVREA).
3. **Species transport:** convection-diffusion-reaction with power-law kinetics (order 0.33 in hydrazine, 1 in catalyst), Arrhenius temperature dependence and a photocatalytic term proportional to the LVREA.

**Mesh independence:** four refinement levels, peak velocity 0.4358, 0.4748, 0.4897 and 0.4896 m/s from Normal to Extra Fine. The Finer mesh was used for all runs.

## What the model showed

- **Dark:** the concentration field is radially symmetric and the light term is zero everywhere, as it should be. I used this as a consistency check.
- **18 mL flask with a quarter-arc UV boundary:** consumption is confined to the lit sector (minimum 2.98 M after 75 min, from 3.3 M), and hydrogen builds up in the same place, consistent with the stoichiometry.
- **150 mL reactor:** consumption forms a ring around the lamp, and the outer region barely reacts.
- **Irradiance sweep (5,000, 10,000, 13,918 and 15,000 W m⁻² sr⁻¹):** the minimum hydrazine concentration drops from 3.08 M to 2.98 M, then does not improve at 15,000.

## Takeaway

Past a point, more light does not help. The model suggests the limit is how well charge carriers reach the Rh sites, and that most of the reactor volume gets little or no UV. Gains should come from better charge separation (for example heterojunction supports like TiO₂-NiO, or better Rh dispersion) and from a different lighting geometry, not from a stronger lamp.

It is the kind of finding I like most: find the real constraint before adding capacity.

## Limits and what is not done

- **2D model with a frozen rotor.** It neglects axial effects such as catalyst settling and does not capture transient stirrer dynamics.
- **Optical coefficients come from the literature**, not from measurements on these catalysts.
- **Catalyst characterization (XRD, TEM, DRS UV-vis) was not complete** when the thesis was written, so its properties are discussed from the literature on similar catalysts.
- **No UV run with Rh/TiO₂-P25 in the 18 mL reactor.** The UV picture there comes from the model, compared against the dark experiments.
- **Quantitative validation of the model against the UV-vis concentration data is still to do.** The agreement so far is qualitative: where the consumption zone is and how the fields look in each geometry.

Next steps in the thesis: a 3D model, a transient stirrer model, measured optical properties, and the quantitative validation.

## Credits

The model builds on earlier CFD work of the supervising group (Adamou et al., 2024 and 2025). The thesis acknowledges doctoral researcher Panagiota Adamou for help with the computational stages.

## Tools

COMSOL Multiphysics 5.5 (Turbulent Flow k-ε, Radiation in Participating Media, Transport of Diluted Species) · catalyst synthesis (wet impregnation, H₂ reduction) · UV-vis spectrophotometry · pressure-based gas monitoring

Full thesis available on request: [LinkedIn](https://www.linkedin.com/in/charilaos-p-stavrou-648a25249)
