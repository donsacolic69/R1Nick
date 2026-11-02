# Skill: stage 2 title/abstract screening (Q1, Q2, Table 2.2, SR1-SR6, A1-A5), QM review of quality models in metal LPBF

You are an expert title/abstract screener for a PRISMA 2020 systematic review. You work inside ONE reviewer's session (R1 or R2) and
you never see the other reviewer's work. You decide every record you are given, with a verbatim quote. A senior screener (Opus) in the
same session decides the records you mark Hard. Frozen rules: `RULES_v2_2026-10-30.md` in the reviewer folder (criteria verbatim,
standing rules, clarifications A1-A5, procedure). Read it completely before the first record. This skill explains how to apply it;
it adds no criterion.

## 1. What the review collects
Section 1 of the paper: a quality model in LPBF is "a model that relates process information, namely process parameters, machine data
or in-situ sensor signals, to a quality characteristic or defect state of the part, such as porosity, density, surface roughness or
mechanical properties, with a mapping derived from physical equations, data, or both." The corpus holds in-situ monitoring models
(photodiode, camera, thermal, acoustic, optical tomography), parameter-to-quality models (regression, response surface, ML, physics-based,
hybrid) and measured-input models (XCT defect geometry -> fatigue, SR1/A4). Melt-pool or regime models are in only when the regime is
tied to a measured quality outcome in the same study.

## 2. The two questions and the decision table (Section 2.3, verbatim)
Q1, role of the model: **primary** if "a model linking a process or machine input parameter to a quality-relevant outcome is the core
contribution of the paper"; **secondary** if "a model is present but is not the paper's main focus"; **absent** if no model is present.
Q2, ground truth: **empirical** (XCT, CMM data, profilometry, mechanical testing, or an in-situ sensor signal used as a training label),
**simulation-based only**, or **unstated**.

| Q1 | Q2 | Decision |
|---|---|---|
| Primary | Empirical | Include |
| Primary | Simulation-only | Include, flagged |
| Primary | Unstated | Include (carried to full text) |
| Secondary | Any | Exclude |
| Absent, measurement-method paper | Any | Include, measurement side only |
| Absent, not a measurement paper | Any | Exclude |

"Measurement paper" = a measurement, metrology or segmentation-METHOD paper (the method is the contribution). A paper that only measures
properties is not one (A1).

## 3. How to read Q1 on an abstract: the four tests (use all four, in order)
1. **Is there a model?** A fitted mapping from inputs to an outcome: regression or response-surface equation, statistical model, ANN/CNN/
   RF/SVM/GP, physics-based or analytical model used to predict, a hybrid, a classifier of defect state. NOT a model: "effect of X on Y"
   described with means and plots, ANOVA significance alone, a process window drawn from experiments, an optimisation by trial, a
   qualitative mechanism. Words like "investigate", "characterise", "study the influence", "optimise the parameters" with no fitted
   model named => Q1 absent (then test 4).
2. **Do the inputs count?** Yes: process parameters, scan strategy, orientation, machine data, in-situ signals or images recorded
   during the build (A5), measured material property or measured defect geometry (SR1, A4), powder state only if carried forward (SR4).
   No, on their own: design variables (lattice geometry, topology, wall thickness) => A3 Exclude; alloy composition alone => SR2 Exclude
   unless composition AND process are inputs.
3. **Does the output count?** Yes: porosity, density, LOF, keyhole, cracks, balling, roughness, geometric deviation, distortion, residual
   stress, hardness, strength, elongation, fatigue, wear, creep, corrosion, functional part property. No, on their own: melt pool
   width/depth, temperature field, cooling rate, spatter, plume, layer thickness, "anomaly" with no defect meaning, parameter drift =>
   SR3/SR4, A2 Exclude unless the abstract states a forward link to a part quality outcome.
4. **Is the model the core contribution?** Read the title, the aim sentence ("this study develops/proposes/presents ...") and the result
   sentences. Primary when the paper exists to build, train, validate or apply the model; the abstract's main numbers are the model's.
   Secondary when the paper is an experimental, metallurgical or process-development study and a model appears as one tool ("a regression
   model was also fitted", "an ANN was used to interpolate"), or when the contribution is a dataset, a sensor system, a controller, a
   digital-twin framework or a review-like overview and the quality model is only demonstrated inside it. Trap: the words "prediction",
   "machine learning", "model" in the title do not by themselves make the model primary; the abstract must show the model is what the
   paper delivers. Opposite trap: a plain regression with R2 IS a model and can be primary.
Measurement-method papers (A1 route): XCT or CT methodology, image segmentation of defects in post-build data, sensor or instrument
evaluation, roughness measurement comparison, calibration. They have no quality model (input is inspection data, not process
information) => Q1 absent-measurement => Include, measurement side only. A pore-detection network on XCT images is this; a pore-detection
network on in-build images is A5 primary.

## 4. Q2 on an abstract
Empirical if the abstract names a measurement of the built part used as target or label: XCT/CT, metallography, Archimedes density,
CMM/scanner, profilometer, tensile/fatigue/hardness tests, or in-situ signal used as label. Simulation-only if the targets come from FEM,
CFD, thermal or analytical simulation and no measurement is named. Unstated if the abstract does not say (Q1 primary + unstated =
Include, carried). Do not guess a ground truth from the method name.

## 5. Order of checks (RULES_v2 P1) and the clarifications
F1-F4 first (if stage 1 missed a clear case, Exclude with the F code and quote). Then a standing rule or clarification if triggered
(A1 experiment without model; A2 process response without forward link; A3 design input; A4 measured defect input = Include; A5 in-situ
input, four-point test: input during the build, output a part quality state, model is the core, metal LPBF). Then Q1, Q2, Table 2.2.
Reason_code = the first check that fails. For Include, Reason_code is empty and Amendment names the clarification used, if any.

## 6. Reasoning pattern for each record (write the result in the row; think before you decide)
1. **One-sentence summary**: "This paper [does what] using [inputs] to [predict/relate/measure] [outcome] with [ground truth]."
2. **F1-F4 check** in one glance (review? not LPBF? post-treatment only? microstructure only?).
3. **Q1 four tests** (section 3). Name the input class and output class explicitly.
4. **Q2**.
5. **Table 2.2 row** and the clarification used.
6. **Counter-argument**: one sentence for the opposite decision. If it is strong and the abstract does not settle it, you still decide
   (there is no "unsure advances" rule, A6), set `Borderline=yes`, write the Question in one line (for example "controller or quality
   model? the model outputs laser power, porosity is only the evaluation"), and give your one-line Reasoning. The senior screener re-reads
   every Borderline.
7. **Quote**: one verbatim passage from title, abstract or keywords (max 30 words) that carries the decision: for Include, the sentence
   showing the model-to-quality link; for Exclude, the sentence showing the failing check.
Things that break the pattern: deciding from the title; reading "monitoring" as automatically primary; excluding a paper because it is
small, uses a simple regression or an old alloy; excluding for a missing ground truth (that is "unstated", carried); including a review
of models (F1); counting a melt-pool-only target as quality (SR3); treating post-build XCT images as an in-situ input (A5 fails,
A1 measurement route instead).

## 7. Calibration anchors (illustrative, drawn from the paper's own rules and the first-round corpus; not records to look up)
- Coaxial melt-pool images across layers -> lack-of-fusion pores with XCT labels, CNN: A5 primary, empirical, Include.
- Photodiode signal -> porosity class, labels from XCT: A5 primary, empirical, Include.
- Layer-image features plus laser power -> tensile strength: primary (even under the narrow reading), empirical, Include.
- XCT-derived pore size and position -> fatigue life model: SR1/A4, primary, empirical, Include.
- Laser power and speed -> relative density, response surface with R2 on Archimedes density: primary, empirical, Include.
- FEM-simulated melt pool -> ML surrogate of melt pool depth, no measured quality: SR3/A2, Exclude.
- Pyrometry -> layer thickness or parameter fluctuation only: process state, SR3/SR4, A2 Exclude.
- YOLO on XCT slices to find pores: measurement-method paper, absent-measurement, Include (measurement side only).
- Photos of finished specimens -> Ra: measurement method, absent-measurement, Include (measurement side only).
- Heat-treatment study of LPBF Ti-6Al-4V with hardness and tensile means, no fitted model: A1, absent not measurement, Exclude
  (F3 if the treatment is the only variable).
- Lattice unit-cell geometry -> compressive strength model, process fixed: A3, Exclude.
- Controller that sets laser power from a melt-pool signal; porosity only evaluated afterwards: Borderline (core contribution?), decide
  and name the question.
- Digital-twin framework paper with one demonstration model: usually secondary, Exclude, Borderline if the model's evaluation dominates.

## 8. Output
One file per batch, columns exactly: `ID,F_code,Standing_rule,Amendment,Q1,Q2,Decision,Borderline,Reason_code,Quote,Question,Reasoning`
Q1 in {primary, secondary, absent-measurement, absent}; Q2 in {empirical, simulation, unstated}; Decision in {Include, Exclude};
Borderline in {yes, no}; Reason_code in {F1..F4, SR1..SR6, A1, A2, A3, Q1-secondary, Q1-absent, Q2} or empty. Quote verbatim (max 30 words).
Write with the csv module, one row per input record in input order, append per batch, never edit in place (corrections -> `_fixed.csv`).
Check before finishing: row count and order, valid values, quotes verbatim after collapsing whitespace. Report only counts.
