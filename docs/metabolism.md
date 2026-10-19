<div class="alert alert-secondary" role="alert" markdown="1">
Part of the [model](model). Status labels: **[computed]** produced in this study; **[literature]** taken from a published source; **[hypothesis]** reasoned but untested; **[pending]** not completed. **None of the values on this page has been validated against wet-lab data.**
</div>

## Step 4. Whole-cell metabolic analysis {#metabolism}

<div class="brief" markdown="1">
<div class="brief-h">In brief</div>

Flux balance analysis, a way of calculating the most a cell's metabolism could produce, was applied to a genome-scale yeast model. The model reaches myristic acid only by breaking down longer fatty acids, output falls as growth is required, and no gene deletion tested beat the unedited strain. The model cannot represent the intended V1254W mutation at all. **[computed]**
</div>

**Question.** Which quantity of C14:0 can the cell reach in the model, at what cost to growth, and by which route? The analyses used flux balance analysis (FBA)[@orth2010|FBA principles and assumptions] on Yeast9[@zhang2024|model used] with COBRApy[@ebrahim2013|software used]. Run conditions are given in the [Data](model#m3) section of the model overview.

**Scope of this page.** Everything here describes the *native* network: the routes to C14 that Yeast-GEM already contains. Yeast-GEM represents fatty acid synthase as reactions terminating at C16:0-CoA and C18:0-CoA, so it has no reaction for early C14 release and **cannot represent the property that FAS2 V1254W is intended to change**. A positive C14 flux in this model is therefore not evidence that the mutation works. The separate reaction-added exercise that attempts to model early release is on the [Bridge](bridge) page and is not part of these results.

**Two naming axes are used throughout, and they are independent.** The *run* is either the **report run** (BY4742, glucose uptake 1.1 mmol gDW⁻¹ h⁻¹) or the **pre-flight run** (prototroph, glucose uptake 1.0). Within either run, the *ligase scenario* is either **forward-only**, the primary scenario, in which the fatty-acid–CoA ligases are restricted to the activating direction, or **shipped bounds**, the sensitivity case, in which they keep the reversibility of the released model.

## Production capacity against growth {#production-capacity}

<div class="brief" markdown="1">
<div class="brief-h">In brief</div>

In the unedited model, free myristic acid can be exported at any growth rate below the maximum, and output falls as more growth is required: 0.227 at 10 % of maximum growth to 0.025 at 90 % (mmol per gram dry weight per hour). At maximum growth the model makes none, so production always costs growth. **[computed]**
</div>

**[computed]** The values below are from the FBA report run: Yeast-GEM v9.1.1, the BY4742 representation, glucose uptake 1.1 mmol gDW⁻¹ h⁻¹, unlimited oxygen and non-growth maintenance of 0.7 mmol ATP gDW⁻¹ h⁻¹ (see [Data](model#m3)). Maximum growth is 0.09768229 h⁻¹ with forward-only ligases and 0.09769 h⁻¹ with the bounds as shipped. The quantity is free-myristate (C14:0) export from the native β-oxidation-dependent routes. It is not methyl myristate, not the output of the intended engineered FAS route, and not a measured titre.

<div class="key" markdown="1">

*Table 1. Maximum free-myristate export (mmol gDW⁻¹ h⁻¹) under a minimum growth requirement. Primary scenario: fatty-acid–CoA ligases restricted to the activating direction. Sensitivity scenario: ligase bounds as shipped in the model.*

| Minimum growth | Growth rate (h⁻¹) | Primary: forward-only | Sensitivity: shipped bounds |
|---|---|---|---|
| none | 0 | 0.25001 | 0.25692 |
| 10 % of maximum | 0.00977 | 0.22649 | 0.23274 |
| 25 % | 0.02442 | 0.19036 | 0.19647 |
| 50 % | 0.04884 | 0.12719 | 0.13156 |
| 75 % | 0.07326 | 0.06359 | 0.06578 |
| 90 % | 0.08791 | 0.02544 | 0.02631 |
| 99 % | 0.09671 | 0.00254 | 0.00263 |
| exactly maximum growth | 0.09768 | 0 | 0 |

</div>

**The row without a growth requirement is a zero-growth limit, not a capacity available to a growing culture.** At maximum growth the export is exactly zero, confirmed by a two-step optimisation in which biomass was fixed at its maximum before export was maximised. Any C14 output therefore costs growth.

**No growth coupling.** The minimum possible export is zero at every growth rate in both scenarios, so the model does not demonstrate growth coupling. The network always retains an alternative carbon sink, since carbon not needed for growth can be oxidised to CO₂, and no feasible solution is forced to make C14.

**The trade-off is piecewise linear**, not a single straight line. It is exactly linear above 50 % of maximum growth, where export is proportional to the growth headroom remaining, at 0.0254 mmol gDW⁻¹ h⁻¹ per 10 % of maximum growth; below 25 % the slope is slightly shallower, about 0.024. At the 50 % floor the export of 0.12719 mmol gDW⁻¹ h⁻¹ corresponds to a mass yield of 0.147 g myristic acid per g glucose.

<figure class="figure my-4">
  <img src="/static/figures/feasibility_frontier.png" class="figure-img img-fluid" alt="Line chart of maximum C14 export against growth held, falling from 0.211 at 10 percent to 0.024 at 90 percent. Wild type and two knockout sets overlap; sets containing POX1 are at zero.">
  <figcaption class="figure-caption"><strong>Figure 1.</strong> Maximum C14 export against the growth rate held, for wild type and selected knockout sets. No knockout set exceeded the wild-type maximum: FAA1, and DGA1 + FAA1 + LRO1, equalled the unedited strain; FAA1 + FAA4 was 2 % below it; any set containing <em>POX1</em> gave exactly zero. <strong>This plot shows the pre-flight run, not the report run of Table 1</strong>, and is retained for the knockout comparison it carries; redrawing it from the report values is <strong>[pending]</strong>. Model run without the early-release reaction; model-implied, not validated against wet-lab data.</figcaption>
</figure>

## Cross-check against the pre-flight run {#pre-flight-cross-check}

<div class="brief" markdown="1">
<div class="brief-h">In brief</div>

An earlier, independently written pipeline computed the same quantity under different conditions. Its numbers differ by 6–7 %, and that difference is fully accounted for by the glucose uptake and the amino-acid supplements, which makes the two runs a check on each other rather than competing results. **[computed]**
</div>

**[computed]** Two runs of this calculation exist, and they differ in strain, medium and pipeline, not in vintage. Neither supersedes the other.

- **Report run.** Yeast-GEM v9.1.1, BY4742 with His, Leu and Lys supplied, glucose uptake 1.1 mmol gDW⁻¹ h⁻¹. Maximum growth 0.09768 h⁻¹. This is the source of Table 1.
- **Pre-flight run.** The prototrophic wild type, glucose uptake 1.0 mmol gDW⁻¹ h⁻¹, computed by the separate pre-flight tool ([Software](software)). Maximum growth 0.0811 h⁻¹.

*Table 2. Maximum C14:0 export in the pre-flight run at fixed fractions of its own wild-type growth rate. The purity column is reported only by this run.*

| Growth held at | C14:0 export (mmol gDW⁻¹ h⁻¹) | C14:0 share of exported fatty acid |
|---|---|---|
| 10 % of wild type | 0.211 | 100 % |
| 25 % | 0.178 | 100 % |
| 50 % | 0.119 | 100 % |
| 75 % | 0.060 | 100 % |
| 90 % | 0.024 | 100 % |

The report run is 6.0–7.3 % higher at matching growth fractions, and the difference resolves in two steps. Scaling the pre-flight maximum growth of 0.0811 h⁻¹ from a glucose uptake of 1.0 to 1.1 mmol gDW⁻¹ h⁻¹ gives 0.0892 h⁻¹, within 0.3 % of the 0.0895 h⁻¹ that the prototrophic model of the report run reaches at that uptake. The remaining 9.1 % up to 0.09768 h⁻¹ comes from the His, Leu and Lys supplements of BY4742, which donate carbon that a per-glucose yield does not count. Two independently written pipelines agreeing to within 0.3 % once the conditions are matched is the strongest reproducibility evidence available for this calculation. A further internal comparison within the pre-flight run gave 0.209152 against 0.2108 mmol gDW⁻¹ h⁻¹ at or above 10 % growth, 0.8 % apart.

**Product purity is reported only by the pre-flight run.** That run found C14:0 to be 100 % of the exported fatty acid at every growth fraction tested, so purity was never limiting. The report run maximises myristate export alone and does not report a product spectrum, so it neither confirms nor contradicts this. Statements elsewhere on this site that the model produces *pure* myristic acid rest on Table 2 and on no other source.

## Metabolic route to C14:0 {#the-route}

<div class="brief" markdown="1">
<div class="brief-h">In brief</div>

Without the added reaction the model has two routes to myristic acid, both of which run through fat breakdown in the peroxisome. The shorter one, chopping two carbons off palmitic acid (C16:0), carries the flux at every optimum examined. Deleting the gene *POX1* removes both. The original plan of reducing breakdown is therefore inverted relative to what the model predicts. **[computed]**
</div>

**[computed]** At 50 % growth every step of the route that carried flux had the same value (0.1192 mmol gDW⁻¹ h⁻¹ in the pre-flight run), which identifies it as a single unbranched path at that optimum. Written with the reaction identifiers of Yeast-GEM:

C16:0-CoA in the peroxisome → (r_0123, acyl-CoA oxidase, *POX1*) → (r_2251, 2-enoyl-CoA hydratase, *FOX2*) → (r_2268, 3-hydroxyacyl-CoA dehydrogenase, *FOX2*) → (r_0102, 3-ketoacyl-CoA thiolase, *POT1*) → myristoyl-CoA → free C14:0 → (r_1772, *PXA1*/*PXA2*) → (r_1777) → export (r_2193) (Figure B).

Peroxisomal C16:0-CoA is supplied either directly from fatty acid synthase (r_2140) through the ABC transporter r_2221, or by re-activation of free peroxisomal palmitate through the *FAA2* ligase r_0402; the flux trace of the pre-flight run used the second of these. *PXA1* and *PXA2* gate both the entry of C16:0-CoA into the peroxisome (r_2221) and the exit of free myristate from it (r_1772), which is why deleting either abolishes export. The final transport step r_1777 carries no gene association in the model, so secretion of myristate is assumed by the model rather than established (assumption A7).

**The release step depends on the ligase scenario and is not a detail.** Free myristate is formed from myristoyl-CoA in one of two ways. With the ligases restricted to the activating direction — the primary scenario — release is by the peroxisomal thioesterase *TES1* (r_0848), which then carries the whole product flux; deleting *TES1* abolishes export. With the ligase bounds as shipped, the model instead runs the C14 ligase r_0412 backwards, regenerating ATP from myristoyl-CoA. That reverse flux is thermodynamically questionable and is the only reason *TES1* appears dispensable, so the shipped-bounds result must not be read as evidence that *TES1* is not needed. A *tes1*Δ strain is consequently an informative experiment rather than a redundant one.

<figure class="figure my-4">
  <img src="/static/figures/explainer_c14_route.png" class="figure-img img-fluid" alt="Vertical chain of seven boxes from C16:0 (palmitic acid) through hexadecanoyl-CoA, acyl-CoA oxidase (POX1, the committed step), enoyl-CoA hydratase, myristoyl-CoA and free C14:0 to export. Side notes give the ligase-reversal check, deletion of POX1, FOX2, POT1, PXA1 or PXA2 giving exactly zero, the r_0102 blocking result, and the consequence for the plan.">
  <figcaption class="figure-caption"><strong>Figure B.</strong> The route that carried the flux at 50 % of wild-type growth in the model without early release: peroxisomal C16:0-CoA, acyl-CoA oxidase (<em>POX1</em>, the committed step), 2-enoyl-CoA hydratase and 3-hydroxyacyl-CoA dehydrogenase (<em>FOX2</em>), thiolase (<em>POT1</em>), myristoyl-CoA, free C14:0 and export. Deleting <em>POX1</em> gave exactly zero. The figure predates the correction of the reaction chain in the text and omits the dehydrogenase step and the release step; the text is authoritative until it is redrawn (<strong>[pending]</strong>). Free C14:0, not methyl myristate, is modelled. Model-implied; not validated against wet-lab data.</figcaption>
</figure>

The model formed C14:0 by removing one two-carbon unit from C16:0 through β-oxidation, not by termination of synthesis. *POX1* catalyses the committed step, and its deletion therefore gave exactly zero.

**Robustness.** Forbidding reversal of the ATP-driven ligase step lowered production by 2 % in the pre-flight run (0.1192 to 0.1167 mmol gDW⁻¹ h⁻¹); in the report run the same restriction lowers maximum export by 2.7 % with no growth requirement and by 3.1–3.3 % at growth floors of 25–90 %. Loopless FBA and an exact loopless mixed-integer formulation reproduced the operating-point maxima, so internal cycles do not inflate the capacity.

**The second route.** Blocking r_0102 in the report run lowered export at the 50 % growth floor from 0.12719 to 0.10977 mmol gDW⁻¹ h⁻¹, a loss of 13.7 % at no cost in growth, and the model switched to a second route: C18:0-CoA is desaturated by *OLE1*, degraded in the peroxisome to C12, re-elongated to myristoyl-CoA in the endoplasmic reticulum by *ELO1*/*IFA38*/*PHS1*/*TSC13* (r_2154 to r_2175) and returned to the peroxisome. Its final step is an elongation and not a shortening, but it still passes through β-oxidation. Blocking both r_0102 and r_2154 abolished C14 export in both ligase scenarios, at zero growth and at 50 % growth, so these are the only two routes the network contains.

The original plan was to reduce degradation in order to preserve C14:0. In this model, degradation is the only source of C14:0 in the absence of the early-release reaction, so the strategy is inverted relative to the model prediction.

## Intervention screen {#intervention-screen}

<div class="brief" markdown="1">
<div class="brief-h">In brief</div>

All 1,143 single-gene deletions were screened in the model. None forced myristic acid export, and removing genes for peroxisomal fat breakdown abolished it. **[computed]**
</div>

**[computed]**

The result files were regenerated from the model and the reported automated checks passed. This is computational reproducibility, not wet-lab validation.

- All 1,143 single-gene deletions were screened in both ligase scenarios: 965 were viable and 178 lethal (lethal denotes no positive biomass flux, a computational classification and not a prediction of cell death), and 934 of the viable deletions reached the specified growth floor. None forced myristate export at the maximum growth rate of the deleted strain.
- At the 50 % growth floor the primary scenario gave 884 candidates with export unchanged, 43 partially reduced and 7 abolished; the sensitivity scenario gave 883, 45 and 6. No candidate increased export.
- Of the 432 ranked candidates, 356 of the 427 viable ones — including the unmodified reference — tied at the 50, 75 and 90 % growth floors in the primary scenario.
- Deletion of *POX1*, *FOX2*, *POT1*, *PXA1* or *PXA2* abolished modelled C14 export, because both C14-producing routes depend on peroxisomal β-oxidation. Deletions of *FAS1*, *FAS2*, *ACC1* and *OLE1* were lethal in the specified medium.
- The genome-wide pass added one further gene whose deletion abolishes export: *MDH3* (YDL078C), which reoxidises inside the peroxisome the NADH generated by the 3-hydroxyacyl-CoA dehydrogenase step, so β-oxidation cannot turn over without it.
- In the primary forward-only scenario, deletion of *TES1* or blocking of r_0848 also abolished export, because the thioesterase is then the only release step. With the ligase bounds as shipped, *TES1* appears dispensable only because the model runs the C14 ligase in reverse instead.
- Blocking individual C14-consuming reactions (r_0125, r_0105, r_2155, r_2195/r_2201, r_2220) changed nothing at 50 % growth, because all carried zero flux at that optimum.
- Combinations were also screened: 189 pairs drawn from a 23-member shortlist, 200 triples and one 13-member stack of C14-consumption and re-activation steps. None raised export at any growth floor. The informative pairs are those combining two individually free deletions that are alternative routes to the same precursor, which lose more than the sum of their members: *acs1*Δ + *acs2*Δ −35.00 %, *zwf1*Δ + *ald6*Δ −27.84 % and *zwf1*Δ + *idp2*Δ −37.76 % at the 50 % floor.
- **A caveat on what this screen can show.** A deletion or a reaction block only removes flux space, so at a fixed absolute growth floor the maximum export of a mutant can only equal or fall below that of the unmodified strain. That no intervention raised export is therefore in large part a property of the method and not a demonstration that improvement is biologically impossible. The screen also cannot see C14 lost in a real cell to futile activation and degradation, which is a question of kinetics and regulation that FBA does not address. The combinations tested were not an exhaustive search.

## Consistency checks {#consistency-checks}

<div class="brief" markdown="1">
<div class="brief-h">In brief</div>

Two ways of writing the cell's growth in the model gave identical results, so one was used throughout. **[computed]**
</div>

**[computed]** The biomass reaction r_2111 and the biomass pseudo-reaction r_4041 carried identical flux in every solution (the biomass metabolite has exactly one producer and one consumer), so either gives the same results. Reaction r_2111 was used throughout, being the default objective of the model.

## Growth-rate penalty {#growth-rate-penalty}

<div class="brief" markdown="1">
<div class="brief-h">In brief</div>

How much each intervention slows growth has now been calculated for the 37 curated interventions of the report run. Most cost nothing at all; the largest penalty among the viable ones is 3.5 %. **[computed]**
</div>

**[computed]** The penalty of an intervention is defined as (1 − μ<sub>max,i</sub> / μ<sub>max,WT</sub>) × 100, where μ<sub>max,WT</sub> is the maximum growth rate of the unmodified model and μ<sub>max,i</sub> that after intervention *i*, both in the same scenario. Of the 37 curated interventions of the report run, 4 were lethal (*fas1*Δ, *fas2*Δ, *acc1*Δ, *ole1*Δ) and 33 viable, of which 29 carried no penalty. The non-zero penalties were *zwf1*Δ 0.41 %, blocking r_0889 0.41 %, *mae1*Δ 0.75 % and blocking r_0112 3.53 %.

Each intervention was evaluated at absolute growth floors of 50, 75, 90 and 100 % of the **unmodified** strain's maximum, never at a fraction of its own maximum, so that a slow-growing deletion is not rewarded with a lower growth demand. Penalties for the full genome-wide screen have not been tabulated on this page. **[pending]**

## Supply constraints and oxygen {#supply-constraints}

<div class="brief" markdown="1">
<div class="brief-h">In brief</div>

Restricting the supply of malonyl-CoA cut export by half, and acetyl-CoA by about a sixth; cofactor supply mattered much less. Raising any of these supplies above its working level changed nothing, so this analysis cannot say whether over-expressing them would help. Oxygen became limiting only when growth was also required. **[computed]**
</div>

**[computed]** Each supply reaction was restricted to a fraction of the flux it carried at the operating point, with the 50 % growth floor held fixed (Table 3).

*Table 3. Change in maximum C14 export at the 50 % growth floor when a supply reaction is limited to half or none of its flux at the optimum (forward-only / shipped-bounds).*

| Reaction | Role | Limited to 50 % | Limited to 0 % |
|---|---|---|---|
| r_0109 | *ACC1*, malonyl-CoA | −53.2 / −53.1 % | growth floor unreachable |
| r_0112 | *ACS1*/*ACS2*, cytosolic acetyl-CoA | −17.3 / −17.6 % | −35.0 / −35.7 % |
| r_0123, r_0102 | C16 → C14 | −6.8 / −5.7 % | −13.7 / −11.5 % |
| r_0466, r_0889 | *ZWF1*/*GND*, NADPH | −2.2 / −2.4 % | −6.5 / −6.9 % |
| r_2140 | FAS, C16:0-CoA | −2.2 / −2.3 % | −4.6 / −4.6 % |
| r_0848 | *TES1*, release | −50 / 0 % | −100 / 0 % |

Export was most sensitive to malonyl-CoA supply through *ACC1*, and *ACC1* is essential: with r_0109 blocked, malonyl-CoA is the only source of the fatty acids the biomass reaction requires, growth falls to zero and the 50 % floor cannot be met. Cytosolic acetyl-CoA supply was intermediate, and oxidative pentose-phosphate NADPH was soft, because *IDP2*, *MAE1* and *ALD6* supply NADPH instead.

**Over-expression could not be assessed.** Raising any of these caps above 100 % changed nothing, which confirms that none of these bounds is binding at the export optimum: the only binding bounds there are glucose uptake, non-growth maintenance and the growth floor. FBA can represent over-expression only as the relaxation of a binding bound, so whether over-expressing *ACC1* or *ACS* would raise C14 cannot be decided from this analysis. Enzyme-constrained modelling or direct measurement would be required.

**Oxygen.** O₂ is unlimited in the modelled condition and does not bind there. A cap of 2.5 mmol gDW⁻¹ h⁻¹ still gave the unlimited-O₂ export. At a cap of 2.0 the export at the 50 % floor fell by 12.9 % (forward-only) and 4.7 % (shipped bounds); at 1.5 it fell further, to 0.0483 and 0.0547 mmol gDW⁻¹ h⁻¹ against 0.1272 and 0.1316 with unlimited O₂. Caps of 1.0 or less made the growth floor unreachable. Without a growth requirement, export at a cap of 2.0 was unchanged. No exact threshold was determined, because no cap between 2.0 and 2.5 was tested. β-oxidation itself consumes O₂ through the *POX1* oxidase, which is why aeration matters here at all.

## Plausibility check against chemostat data {#plausibility-check}

<div class="brief" markdown="1">
<div class="brief-h">In brief</div>

The model's growth predictions were compared with published chemostat measurements. The model under-predicted growth at all four points by 5–11 %, and two of the four fell outside the agreement criterion set in advance. This is a limited check, not a validation, because the published strain is not the one modelled. **[computed]**
</div>

**[computed]** The only verified dataset with comparable conditions is that of Van Hoek and colleagues: aerobic, glucose-limited chemostats of a prototrophic industrial baker's yeast at 30 °C and pH 5.0.[@vanhoek1998|measured glucose uptake, growth, O₂ and CO₂ in glucose-limited chemostats] Each measured glucose uptake was imposed on the prototrophic model and the model's maximum growth compared with the measured steady-state growth rate (Table 4).

*Table 4. Plausibility check against published chemostat data (strain DS28911, not BY4742). Fluxes in mmol gDW⁻¹ h⁻¹. The agreement criterion of ±10 % was fixed before interpretation.*

| Measured D (h⁻¹) | Glucose uptake | Predicted max growth | Error |
|---|---|---|---|
| 0.025 | 0.3 | 0.02218 | −11.3 % |
| 0.05 | 0.6 | 0.04743 | −5.1 % |
| 0.10 | 1.1 | 0.08952 | −10.5 % |
| 0.15 | 1.7 | 0.14002 | −6.7 % |

The failure is one-sided: the model under-predicts at every point, which means it declares the organism's observed growth infeasible at that glucose uptake, and points at the biomass composition or the maintenance values rather than at a random discrepancy. O₂ uptake agreed to within 0.3–12.8 %, and no ethanol was predicted, which is correct in this fully respiratory range. No parameter was tuned. Because the strain differs and the published uptakes are rounded, this is a limited plausibility check and not a validation for BY4742.

Two further limits of the same kind are worth recording. With unlimited O₂, plain FBA predicts no ethanol at any glucose uptake, so it cannot represent the Crabtree effect and batch production conditions lie outside the range examined here. And Yeast-GEM contains 202 unbalanced internal reactions, mostly lipid bookkeeping reactions and respiratory complexes with fractional proton stoichiometry; at non-zero growth these lose carbon equal to about 5.4 % of the carbon retained by the cell, which propagates to an illustrative shift of roughly 3.4 % in export at the 50 % floor. That figure is an assumption-dependent sensitivity estimate and not an error bound, and its direction is unresolved. With no growth requirement the carbon balance closes exactly and the capacity is unaffected.

## Experiments informed by the model {#experiments-informed-by-fba}

<div class="brief" markdown="1">
<div class="brief-h">In brief</div>

The modelling suggests four experiments that would distinguish between competing explanations for any C14 that the engineered strain makes. These are proposals, not completed work. **[pending]**
</div>

**[pending]** None of the following has been carried out. They are listed because the model's structure makes them informative, not because any result is expected.

- **Quantitative C10–C18 fatty-acid profiling** of the engineered strain against the parent BY4742 and an empty-cassette integrant, with internal standards and per-chain calibration, reporting free and lipid-bound fractions separately. Chain capping at C14 would raise C14 and lower C16 with little below C14; chain shortening would also raise C12 and C10.
- **The same profiling in a *pox1*Δ background.** In the model β-oxidation is the only C14 source, so this deletion abolishes C14. In a strain whose FAS really released C14, β-oxidation would instead act mainly as a sink. C14 persisting without β-oxidation would therefore point away from the native route, though it would not by itself prove direct FAS-mediated synthesis.
- **A *tes1*Δ strain**, which tests the ligase-direction question directly. The primary scenario predicts that this abolishes export; the sensitivity scenario predicts no effect.
- **An aeration series**, since the model's capacity falls by 12.9 % at an oxygen cap of 2.0 mmol gDW⁻¹ h⁻¹ when growth is required and not at all when it is not.
- **Separate validation of the ex-cell esterification step.** Fatty-acid methyl ester analysis converts acyl chains into methyl esters, so the enzymatic product must be quantified without that derivatisation, against an authentic methyl myristate standard.

## Reachable set and frontier {#reachable-set-and-frontier}

<div class="brief" markdown="1">
<div class="brief-h">In brief</div>

The same model can also map which fatty-acid mixtures are reachable. The example uses an illustrative target, not a measurement, so it demonstrates the method and does not predict a result. **[computed]**
</div>

**[computed]** The same model supports a reachable-set analysis for a fatty-acid profile and not only for the amount of C14. Figure 2 shows the result for an illustrative C14-rich target; the target is an assumption and not a measurement.

**Provenance.** This analysis asks a different question from the capacity calculation above and does not appear in the FBA report. Its source data, target profile and generation method are **[pending]** a link from this page; until that is supplied it should be read as an additional exploratory analysis rather than as part of the reported native-route results.

<figure class="figure my-4">
  <img src="/static/figures/reachable_c14.png" class="figure-img img-fluid" alt="Left: curve of best achievable distance to the target profile against minimum total fatty-acid titre, flat near zero until a knee at 0.118 and then rising, with an unreachable region shaded above the maximum titre. Right: stacked bars showing fatty-acid composition at selected points on the frontier.">
  <figcaption class="figure-caption"><strong>Figure 2.</strong> Left: best achievable distance to an illustrative C14-rich target profile against the minimum total fatty-acid titre (Yeast9); the shaded region is unreachable. Right: fatty-acid composition at selected points on the frontier. The knee at 0.118 mmol gDW⁻¹ h⁻¹ is the largest titre within the assay's tie band of the target. Model-implied upper bounds; not validated against wet-lab data.</figcaption>
</figure>

---

**Previous:** [Step 3 Bridge](bridge) · **Next:** [Step 5 Trust](trust)
