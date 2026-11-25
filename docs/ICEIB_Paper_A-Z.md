# Traffic Timing Assistant: An Explainable Edge AIoT System for Single-Intersection Signal Control with ARM/FPGA Co-Execution

> **Format:** IEEE Conference (ICEIB Style — `https://www.iceib.asia/`)  
> **Writing Style:** 2020 A–Z SOP Framework (`[A]`–`[Z]`)  
> **Source Basis:** [第13組_Proposal.pdf](../第13組_Proposal.pdf), [README.md](../README.md), [交通專題分析_A-Z.md](./交通專題分析_A-Z.md)

---

## Abstract

- **[A — Attention Getter]** Conventional fixed-time traffic signal controllers are pre-configured from historical averages and fail to adapt dynamically to directional imbalances, temporal demand shifts, and sudden traffic surges.
- **[B — But / Challenge]** Meanwhile, many existing adaptive signal control approaches rely on deep reinforcement learning, large language models (LLMs), or network-wide simulators that are computationally prohibitive and lack decision transparency on resource-constrained edge hardware.
- **[C — Cure]** This paper presents the *Traffic Timing Assistant*, an explainable Domain AI Agent designed for two-axis through-traffic control at an isolated intersection using an ARM/FPGA Artificial Intelligence of Things (AIoT) co-execution architecture.
- **[D — Development]** The system integrates data sufficiency checking, recent-arrival and queue estimation, a compact decision tree selecting among three discrete plans (*Balanced*, *North–South Priority*, and *East--West Priority*), deterministic rule-based fallback for out-of-domain states, cycle-boundary actuation on the FPGA, and hardware readback verification.
- **[E — Experiments]** Under identical synthetic arrival profiles, the proposed policy is benchmarked against a fixed-balanced baseline using Queue Vehicle-Seconds (QVS), average waiting time, remaining unserved vehicles, directional disparity, and hardware execution consistency.
- **[F — Findings]** Preliminary paired host simulations achieve total QVS reductions of 18.28% across 18 scenarios (with 5 degraded cases) and 19.71% across 6 scenarios (with 2 degraded cases), with degraded cases concentrated in balanced and sudden-burst demand regimes, while development-board tests confirm cycle-boundary plan activation and queue reduction in a directional-shift scenario. Because traffic performance is evaluated using simplified first-in, first-out (FIFO) queues, real-world road benefits require separate field validation.

**Index Terms—** Adaptive traffic signal control, Artificial Intelligence of Things (AIoT), explainable decision tree, ARM/FPGA co-design, rule-based fallback, hardware readback verification.

---

## I. Introduction

- **[G — Current State]** Urban intersections rely on traffic signals to allocate shared green time across conflicting directions. When directional demands fluctuate, static fixed-time plans often induce avoidable queues. Recent municipal pilots and empirical traffic studies demonstrate the promise of demand-responsive timing—including Hong Kong's adaptive signal pilot [1] and big-data adaptive signal impact modeling across 100 cities [2].
- **[H — Challenges]** Despite promising results, lightweight edge deployment faces two practical obstacles: (1) displaying traffic counts or toggling lights does not explain *why* a timing plan was chosen or verify *whether* hardware actually executed it; and (2) heavy AI controllers such as spatio-temporal graph networks and LLM-driven agents [3], [4] are difficult to deploy and audit on compact development boards.
- **[I — Literature Categories & J — Literature Critique]** Existing research spans verifiable tree-policy extraction from neural networks (VIPER [5]), multi-intersection or hierarchical LLM controllers [3], [4], urban field pilots and emission modeling [1], [2], and formal signal timing engineering standards (FHWA Manual [6]). However, heavy graph and LLM models target large-scale simulations rather than deterministic single-board execution with verifiable safety interlocks.
- **[K — Core Contributions]** We propose the *Traffic Timing Assistant* scoped to a single intersection with two through-traffic axes and three timing plans (*Balanced*, *N–S Priority*, *E–W Priority*). Our contributions pursue three goals:
  1. **Demand Suitability:** Benchmark decision-tree plus rule-fallback timing against fixed-balanced timing under identical inputs.
  2. **Decision Explainability:** Trace every plan choice to observed arrival/queue features, tree split paths, and explicit fallback triggers.
  3. **Execution Verification:** Read back active plans, phases, and countdown timers from the ARM/FPGA board. Multi-intersection coordination, pedestrian signals, turning lanes, and roadside deployment are explicitly excluded.
- **[L — Paper Organization]** *(Addresses Proposal Gap L)* The remainder of this paper is organized as follows. Section II reviews related AI and traffic domain literature and establishes our research positioning. Section III presents the proposed design, combining domain design rationales, the eight-module ARM/FPGA architecture, workflow, core algorithm, and queue formulation. Section IV details the experimental setup, preliminary host and board results, and validity limits. Section V concludes the paper and outlines future work.

---

## II. Related Work

- **[M — Taxonomy & N — Research Trends]** We review three representative AI control studies ([3]–[5]) alongside three traffic engineering sources ([1], [2], [6]). Across AI methods, work evolves from distilling verifiable decision trees [5] to multi-agent LLM coordination [3] and hierarchical upper/lower control splits [4]. Across traffic engineering, studies progress from practical urban pilots [1] and city-level emission analysis [2] to foundational phase-timing constraints [6].
- **[O — Article Summary Table & Research Gap]**

| Ref | Year | Problem | AI Method | Domain Knowledge | Dataset | Findings | Limitation |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| [1] HK Pilot | 2025 | Pre-timed plans lag demand | AI analytics (details undisclosed) | Time-of-day, direction, vehicle/pedestrian demand | Tung Chung intersection pilot | Motivates adaptive timing in practice | Full controlled comparison not publicly disclosed |
| [2] Wu et al. | 2025 | Signal impact on delay & CO₂ | Data-driven adaptive timing | Flow, capacity, applicability regimes | 100 Chinese cities; CBEngine | Gains vary strongly by city and demand | Simulation estimates cannot transfer directly to our prototype |
| [3] CoLLMLight | 2025 | Multi-intersection coordination | Spatio-temporal graphs, LLM collaboration | Adjacent intersections, demand shifts | Jinan, Hangzhou, NYC; CityFlow | Cooperative reasoning helps tested scenarios | Simulation-only; compute exceeds edge board target |
| [4] VTP | 2026 | Unforeseen incident adjustment | Upper LLM tuning & verification | Incident conditions, lower control knowledge | SUMO single-intersection incidents | Clear upper/lower decision-control split | Preprint; incident handling ≠ road safety certification |
| [5] VIPER | 2018 | Policies hard to inspect | Decision-tree extraction from neural policies | Policy, action values, control properties | Pong, Cart-Pole, control tasks | Tree policies allow inspection and verification | Non-traffic domain; used here only for tree representation |
| [6] FHWA | 2008 | Throughput vs. phase limits | Non-AI engineering standard | Green, yellow, clearance, pedestrians | Engineering formulas and case studies | Foundational timing and evaluation framework | Superseded by newer editions; non-local regulations |

- **Research Gap Positioning:** *Existing Research* covers adaptive urban pilots [1], [2], cooperative/hierarchical LLM control [3], [4], tree policy extraction [5], and timing rules [6]; *Limitations* show high complexity and simulation-only assumptions unsuitable for small embedded demos; *Research Gap* lies in linking data validation, interpretable choice rationale, and hardware readback on constrained boards; *Our Project* integrates a compact decision tree, rule fallback, and ARM/FPGA co-execution benchmarked against fixed timing.

---

## III. Proposed Design

### A. Domain Design Rationale and Trade-offs `[PA–PF]`
Synthesizing [1]–[6] yields five design mindsets and three engineering trade-offs:
- **M1 (Demand-Driven Formulation):** Cover balanced, skewed, and shifting traffic while keeping a fixed baseline [1], [2].
- **M2 (Decoupled Decision & Execution):** ARM performs analytics and plan selection; FPGA enforces phase order and countdown safety [4].
- **M3 (Teacher-Rule Approximation Awareness):** The decision tree imitates domain scoring rules [5]; approximation errors are acknowledged rather than assuming tree superiority.
- **M4 (Evidence-Scoped Claims):** Strictly separate data diagnostics, synthetic FIFO simulation, and hardware readback [1], [3], [4].
- **M5 (Retention of Negative Cases):** Report both improved and degraded scenarios so averages never conceal directional penalties [6].
- **Trade-offs:**
  - **C1 (Rules vs. Decision Tree):** Generate labels from scoring rules, deploy the compact decision tree with out-of-domain rule fallback [5].
  - **C2 (Immediate vs. Cycle-Boundary Switching):** Latch new plans strictly at complete cycle boundaries on the FPGA [4], [6] to preserve countdown integrity.
  - **C3 (Mean Delay vs. Fairness/Completeness):** Report aggregate QVS alongside directional metrics, unserved vehicles, and degraded cases [2], [6].

### B. Eight-Module Closed-Loop Architecture `[PG]`
1. **Module 1 — User & Structured Request** *(Integration Target)*: Specifies input dataset and mode (control vs. review-only).
2. **Module 2 — Data Source & Validation** *(Integration Target)*: Verifies timestamps, units, and history sufficiency; halts on insufficient data.
3. **Module 3 — Analysis Engine** *(Core Ready)*: Computes N–S and E–W recent arrivals and estimated queues.
4. **Module 4 — Decision Tree** *(Core Ready)*: Selects *Balanced*, *N–S Priority*, or *E–W Priority* from the 4 axis features.
5. **Module 5 — Domain Constraints & Fallback** *(Core Ready)*: Enforces legal plans, min/max green, clearance, and out-of-domain rule fallback.
6. **Module 6 — Decision Rationale & Reporting** *(Integration Target)*: Records actual features, tree path or fallback reason, and evaluation summary.
7. **Module 7 — ARM/FPGA Execution** *(Core Ready)*: Submits validated plans from ARM to FPGA for next-cycle commitment.
8. **Module 8 — Readback & Display** *(Core Ready)*: Reads back active plan, phase, and countdown, sending *execution evidence* to Module 6 and *state feedback* to Module 3.

### C. Workflow and Core Algorithm `[PH–PI]`
1. `Read task mode and traffic data`
2. `If data is insufficient: report the gap and stop`
3. `For each observation: update queues and recent arrivals`
4. `If not at a decision boundary: continue`
5. `If features are in-domain: select plan with the tree`
6. `Else: select plan with fallback rules`
7. `Record actual features, decision path and fallback reason`
8. `If review-only mode: report recommendation and continue`
9. `If plan or device state is invalid: report and continue`
10. `Submit plan; apply it at the next complete cycle`
11. `Read back the applied plan; report success or mismatch`
12. `Summarize decisions, execution results and limitations`

Separating data sufficiency (Line 2), domain applicability (Line 5), and hardware readback (Lines 10–11) ensures full stage-by-stage traceability.

### D. Case Design and Queue Formulation `[PJ–PM]`
Restricting outputs to three discrete timing plans (*Balanced*, *N–S Priority*, *E–W Priority*) driven by recent arrivals and estimated queues makes both decision-tree inspection and FPGA phase verification tractable. Under discrete-time FIFO queue conservation over horizon $T$ seconds:

$$q_d(t+1) = \max\bigl(0,\, q_d(t) + a_d(t) - s_d(t)\bigr), \quad d \in \{\text{NS}, \text{EW}\}$$

$$\text{QVS} = \sum_{t=1}^{T} \left( q_{\text{NS}}(t) + q_{\text{EW}}(t) \right)$$

---

## IV. Experiment

- **[Q — Metrics]** Primary metric: QVS (lower is better). Auxiliary metrics: average waiting time (read alongside remaining unserved vehicles), directional disparity, and hardware readback consistency.
- **[R — Baseline]** Identical arrival and service conditions comparing *Fixed Balanced Timing* against *Decision Tree + Rule Fallback*.
- **[S — Scenarios]** Five synthetic evaluation regimes:

| Traffic Regime | Demand Profile | Evaluation Objective |
| :--- | :--- | :--- |
| Balanced Flow | Comparable N–S and E–W arrivals | Verify whether adaptive switching avoids unnecessary overhead |
| Unidirectional Skew | Persistent priority on one axis | Test green reallocation toward dominant queue |
| Directional Shift | Dominant axis reverses mid-run | Evaluate responsiveness across cycle-boundary switching |
| Sudden Burst Spike | Short-duration arrival surge | Stress-test hysteresis and fallback boundary behavior |
| Overload Condition | Arrivals exceed total capacity | Verify out-of-domain rule fallback and unserved-vehicle reporting |

- **[T — Ongoing Parameter Sweeps & Integration]** Integration of Modules 1, 2, and 6 alongside systematic parameter sweeps across green splits and board-level timing latency remains ongoing work.
- **[U — Preliminary Results]**

| Test Suite | Observed Summary | Engineering Implication |
| :--- | :--- | :--- |
| Host Paired Batch 1 (18 scenarios) | Total QVS reduced by **18.28%**; **5 cases degraded** | Performance varies by regime; negative counterexamples must be preserved |
| Host Paired Batch 2 (6 scenarios) | Total QVS reduced by **19.71%**; **2 cases degraded** | Balanced and sudden-burst scenarios remain primary tuning targets |
| Dev-Board Paired Test | Cycle-boundary plan activation verified; QVS reduced in directional-shift test | Confirms ARM/FPGA closed-loop execution; multi-scenario board testing needed |

- **[V — Validity & Limitations]** All quantitative traffic results come from synthetic inputs and a simplified FIFO model, not field road tests. Official minute-level traffic datasets are currently insufficient for continuous dual-axis per-second control evaluation and are therefore limited to data-quality diagnostics.

---

## V. Conclusion

*(Addresses Proposal Gap W–Z)*

- **[W — Restate Significance]** The *Traffic Timing Assistant* addresses the need for lightweight, transparent, and hardware-verifiable adaptive signal control at an isolated intersection.
- **[X — Methodological Distinction]** By coupling a compact decision tree with out-of-domain rule fallback and ARM/FPGA cycle-boundary co-execution, the system guarantees deterministic phase safety and auditable decisions without heavy LLM or DRL overhead.
- **[Y — Deliverables & Outcomes]** The prototype delivers an end-to-end decision, rationale, and hardware readback workflow supported by paired synthetic benchmarks (`-18.28%` and `-19.71%` total QVS reductions, explicitly reporting 5/18 and 2/6 degraded cases) and verified board-level plan switching.
- **[Z — Limitations & Future Work]** Future work will (1) conduct root-cause ablations on the degraded cases observed in both host batches (5 of 18 and 2 of 6), particularly balanced and burst-demand scenarios, (2) acquire continuous per-second empirical sensor logs to replace FIFO approximations, and (3) extend the model to pedestrian phases, turning movements, sensor noise robustness, and multi-intersection coordination.

---

## References

1. Information Services Department, Hong Kong SAR Government, "Adaptive system optimises traffic flow," Nov. 23, 2025. https://www.news.gov.hk/eng/2025/11/20251120/20251120_183103_322.html?type=ticker
2. K. Wu *et al.*, "Big-data empowered traffic signal control could reduce urban carbon emission," *Nature Communications*, vol. 16, art. 2013, 2025. https://doi.org/10.1038/s41467-025-56701-4
3. Z. Yuan, S. Lai, and H. Liu, "CoLLMLight: Cooperative Large Language Model Agents for Network-Wide Traffic Signal Control," *arXiv:2503.11739v1*, 2025. https://arxiv.org/abs/2503.11739v1
4. S. Wei, Q. Wang, and K. Yang, "Virtual Traffic Police: Large Language Model-Augmented Traffic Signal Control for Unforeseen Incidents," *arXiv:2601.15816v1*, 2026. https://arxiv.org/abs/2601.15816v1
5. O. Bastani, Y. Pu, and A. Solar-Lezama, "Verifiable Reinforcement Learning via Policy Extraction," *NeurIPS*, vol. 31, 2018. https://proceedings.neurips.cc/paper/2018/hash/e6d8545daa42d5ced125a4bf747b3688-Abstract.html
6. P. Koonce *et al.*, *Traffic Signal Timing Manual*, Federal Highway Administration (FHWA), Rep. FHWA-HOP-08-024, 2008. https://ops.fhwa.dot.gov/publications/fhwahop08024/fhwa_hop_08_024.pdf
