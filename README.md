# A Stochastic Framework for Understanding Long-Latency Inference in Complex Systems


> **Key Idea:** Using population simulation and counterfactual perturbation to study delayed, partially observed risk, developed through an application to young-onset rheumatoid arthritis.

---
 
## Research Question

How can we infer the population-level consequences of an exposure when its effects are delayed, exposure histories are incomplete, and the counterfactual outcome cannot be observed directly?

This question emerged from studying obesity and young-onset rheumatoid arthritis, reframing a biological problem as one of long-latency inference under uncertainty.

---

## Research Evolution

Stage I — Biological Question → Computational Model (Jan 2025 – Jun 2026)

The project began with a biological question and moved to stochastic simulation when conventional observational approaches could not capture long-latency effects.

Stage II — Computational Model → Mathematical Inference Framework (Summer 2026)

The focus shifted from rheumatoid arthritis itself to the underlying problems of stochastic modeling, counterfactual inference, parameter uncertainty, and validation. This repository preserves that framework.

Stage III — Empirical Validation and Methodological Extension (Sep 2026 – Present)

Current work moves to patient-level longitudinal data to test the framework empirically and identify where deeper statistical or mathematical methods are needed.

---

## Mathematical Framework

The model treats long-latency risk as a stochastic population-level inference problem. A synthetic population is generated from specified demographic and exposure distributions, individual disease probabilities are constructed from parameterized risk contributions, and outcomes are sampled probabilistically. Counterfactual perturbations are then applied to exposure distributions to examine how changes at the individual level propagate into population-level disease patterns.

The framework has five main components: a synthetic population model, an individual risk model, a long-latency exposure model, counterfactual perturbation, and Monte Carlo estimation under parameter uncertainty.

---

### Synthetic Population Model

The model generates \(N=1{,}000{,}000\) synthetic individuals,

$$ X_i=(A_i,B_i,G_i,S_i), $$

representing age, BMI, genetic risk, and smoking exposure. These characteristics are sampled probabilistically to create heterogeneous risk profiles for population-level simulation and counterfactual testing.

---

### Individual Risk Model

Individual disease risk is modeled on the log-odds scale:

$$ z_i=\beta_{0,i}+\beta_{G,i}+\beta_{SG,i}+\beta_{A,i}+\beta_{B,i}. $$

For model parameters \(\theta\),

$$ p_\theta(X_i)=P(Y_i=1\mid X_i,\theta)=\frac{1}{1+e^{-z_i}}. $$

Disease status is then sampled as a Bernoulli outcome, preserving stochastic variation at the individual level.

---

### Long-Latency Exposure Model

BMI-associated risk is allowed to decay with age through

$$ a_i=e^{k\max(A_i-15,0)}, $$

with \(k<0\). The corresponding BMI odds ratio is

$$ OR_i=1+(OR_{\max}-1)a_i. $$

This makes the exposure contribution strongest near the reference age and progressively weaker over time.

---

### Counterfactual Perturbation

The framework perturbs the BMI distribution of individuals under age 25 while holding the remaining model structure fixed. If \(T_\delta\) denotes the exposure perturbation, the population-level response is

$$ \Delta_\theta(\delta) = \mathbb{E}_X \left[ p_\theta(T_\delta(X))-p_\theta(X) \right]. $$

This represents a model-based counterfactual response under stated assumptions, not a directly identified causal effect.

---

### Monte Carlo Estimation and Uncertainty

Population-level outcomes are estimated across 2,500 bootstrap trials. For a statistic \(T\), the simulation produces

$$ T^{(1)},T^{(2)},\ldots,T^{(2500)}, $$

with the median reported as the central estimate and the 2.5th–97.5th percentiles used as uncertainty bounds.

The resulting variation reflects stochastic outcome generation and uncertainty in selected model parameters; structural assumptions are evaluated separately through sensitivity analysis.

---

## Rheumatoid Arthritis as the Testbed

Young-onset rheumatoid arthritis serves as the application domain for the framework because relevant exposures may precede diagnosis by years and exposure histories are only partially observed.

Literature-derived estimates for baseline prevalence, smoking, genetic risk, and interaction effects parameterize the model, while BMI is treated as the primary exposure for counterfactual perturbation.

---

## Computational Implementation

The core simulation engine is implemented in Java, with Python notebooks used for analysis, sensitivity testing, and visualization. Major simulation parameters are exposed explicitly and a fixed random seed supports reproducibility.

---

## Sensitivity, Validation, and Limits

Sensitivity analysis varies younger-population BMI and the latency-decay parameter to test dependence on structural assumptions. Simulated prevalence is compared with aggregate population estimates as a form of model checking.

The framework evaluates counterfactual behavior under stated assumptions; it does not identify a causal effect, establish the true biological latency mechanism, or uniquely validate the model from aggregate agreement. These limitations motivate Stage III validation with patient-level longitudinal data.

---

## Repository Structure

- `src/SimulationEngine.java` — core Java simulation engine
- `analysis/risk_model_analysis.ipynb` — primary analysis notebook
- `analysis/figures.ipynb` — visualization and sensitivity-analysis notebook
- `Data/` — saved outputs from BMI and latency-decay sensitivity experiments
- `Graphs/` — figures generated from the analysis
- `artifacts/` — related research artifacts
- `README.md` — mathematical framing, research trajectory, and repository guide

This structure intentionally separates the simulation model, analysis, and preserved results so the framework can be inspected as a self-contained reference.

---

## Related Research Artifacts

These artifacts document the original application-driven phase of the project:

**[Preprint (bioRxiv)](https://doi.org/10.64898/2026.01.29.702692):** application-focused manuscript on obesity and young-onset rheumatoid arthritis 

**[AAI Midwinter Conference Poster](artifacts/AAIMidwinterConference2026_poster.pdf):** presentation of the original modeling work 

**[Research Process Essay](artifacts/Process_Essay.pdf):** account of the research and model-development process behind the original study

---

## Status and Next Stage

This repository preserves the Stage II stochastic framework before empirical longitudinal validation. Stage III continues separately using patient-level data to test where the framework holds, where it fails, and what additional statistical or mathematical methods are required.

---

## Authorship

The simulation framework, implementation, analysis, and visualizations in this repository were developed by Tyler Hatstadt as part of the research described in the associated preprint.
