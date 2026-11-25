# ICEIB IEEE Conference Paper — 2020 A–Z SOP Writing Guide

> Source framework: [交通專題分析.pdf](./交通專題分析.pdf) & [交通專題分析_A-Z.md](./交通專題分析_A-Z.md)  
> Target venue: IEEE International Conference on Electronic Communications, Internet of Things and Big Data ([ICEIB](https://www.iceib.asia/))  
> Target deliverables: [ICEIB_Paper_A-Z.md](./ICEIB_Paper_A-Z.md) (A–Z annotated Markdown) & [ICEIB paper/main.txt](../ICEIB%20paper/main.txt) (`IEEEtran` LaTeX)

---

## 1. IEEE ICEIB Conference Formatting Requirements

| Item | Requirement |
| :--- | :--- |
| **Template Class** | `\documentclass[conference]{IEEEtran}` (double-column, single-spaced, 10 pt Times body text) |
| **Page Length** | Typically **4–6 pages** including figures, tables, and references (verify active cycle on `iceib.asia`) |
| **Page Size & Headers** | Standard US Letter or A4 per active ICEIB CFP; omit running page numbers on final camera-ready PDF |
| **Required Sections** | `Abstract`, `Index Terms`, `I. Introduction`, `II. Related Work`, `III. Proposed Design`, `IV. Experiment`, `V. Conclusion`, `References` |
| **Citation Style** | Numbered IEEE citations in square brackets (`[1]`–`[6]`), ordered by appearance |
| **Empirical Honesty** | Do not fabricate road measurements; report simplified FIFO simulation results alongside degraded/negative cases |

---

## 2. Complete A–Z Mapping onto ICEIB Paper Sections

### Part 1: `Abstract` (A–F)

| Code | A–Z Element | Required Content in *Traffic Timing Assistant* |
| :--- | :--- | :--- |
| **A** | Attention Getter | Fixed-time signals fail under directional skew, temporal demand shifts, and surges (citing Maricopa/HK motivation). |
| **B** | But (Challenge) | Existing DRL/LLM/network-wide adaptive methods are too heavy and opaque for constrained edge hardware. |
| **C** | Cure | *Traffic Timing Assistant*: Domain AI Agent for single-intersection two-axis through-traffic with ARM/FPGA co-execution. |
| **D** | Development | Closed-loop pipeline: data check, arrival/queue estimation, compact decision tree (`Balanced`, `N–S Priority`, `E–W Priority`), rule fallback, cycle-boundary actuation, readback. |
| **E** | Experiments | Paired comparison vs. fixed-balanced baseline on QVS, wait time, remaining vehicles, directional disparity, and board readback. |
| **F** | Findings | Host paired tests: `-18.28%` QVS (18 cases, 5 degraded) & `-19.71%` QVS (6 cases, 2 degraded); board activation verified; FIFO limitation stated. |

### Part 2: `I. Introduction` (G–L)

| Code | A–Z Element | Required Content in *Traffic Timing Assistant* |
| :--- | :--- | :--- |
| **G** | Current State (現況) | Shared green time under fixed plans; real-world adaptive motivation from HK pilot `[1]` and 100-city study `[2]`. |
| **H** | Challenges (挑戰) | Two gaps: lack of decision explainability/execution auditability, and compute/safety limits of complex AI on embedded boards. |
| **I** | Literature Categories (文獻分類) | Policy distillation (`VIPER`), multi-agent/hierarchical LLM (`CoLLMLight`, `VTP`), and domain pilots/standards (`HK`, `Wu et al.`, `FHWA`). |
| **J** | Literature Critique (文獻評述) | Complex graph/LLM methods exceed single-board resources and lack deterministic phase interlocks. |
| **K** | Core Contributions (核心貢獻) | Three objectives: demand suitability, decision explainability, and hardware readback verification; strict single-intersection scope. |
| **L** | Paper Organization (章節導覽) | **Fixes Proposal Gap L:** Explicit roadmap summarizing Sections II–V at the end of Section I. |

### Part 3: `II. Related Work` (M–O)

| Code | A–Z Element | Required Content in *Traffic Timing Assistant* |
| :--- | :--- | :--- |
| **M** | Taxonomy (文獻分類) | Balanced 1/2 AI (`[3]`–`[5]`) + 1/2 Traffic Domain (`[1]`, `[2]`, `[6]`). |
| **N** | Research Trends (趨勢與脈絡) | Progression from neural-to-tree distillation, multi-intersection LLMs, and hierarchical control to city-scale impact and FHWA phase rules. |
| **O** | Comparison Table & Gap (比較與缺口) | 8-column `Article Summary Table` (`Ref`, `Year`, `Problem`, `AI Method`, `Domain Knowledge`, `Dataset`, `Findings`, `Limitation`) + `Existing → Limitations → Gap → Our Project`. |

### Part 4: `III. Proposed Design` (P / PA–PM + Domain Deep Research)

| Code | A–Z Element | Required Content in *Traffic Timing Assistant* |
| :--- | :--- | :--- |
| **PA–PF** | Design Rationale & Mechanisms | Five mindsets (`M1`–`M5`), three engineering trade-offs (`C1`–`C3`), compact decision tree + rule fallback. |
| **PG** | Architecture & Module IDs | 8-module closed-loop ARM/FPGA pipeline (`Modules ①–⑧`), distinguishing Core Ready vs. Integration Targets with state & evidence feedback. |
| **PH–PI** | Workflow & Pseudocode | Decision-boundary gating, three separated validation gates, and line-numbered 12-line `Algorithm 1`. |
| **PJ–PK** | Case Scope & Contributions | Three discrete plans (`Balanced`, `N–S Priority`, `E–W Priority`) driven by 4 axis features (`N–S/E–W arrivals & queues`). |
| **PL–PM** | Simulation & Queue Formulation | Synthetic FIFO queue conservation formulation and `QVS` definition: $\text{QVS} = \sum_{t=1}^{T}(q_{\text{NS}}(t) + q_{\text{EW}}(t))$. |

### Part 5: `IV. Experiment` (Q–V)

| Code | A–Z Element | Required Content in *Traffic Timing Assistant* |
| :--- | :--- | :--- |
| **Q** | Evaluation Metrics (指標) | Primary: Queue Vehicle-Seconds (`QVS`); auxiliary: avg waiting time (with remaining vehicles), directional disparity, readback match. |
| **R** | Baseline (比較基準) | Fixed Balanced Timing vs. Decision Tree + Rule Fallback under identical arrival sequences. |
| **S** | Scenarios (情境設定) | Five synthetic regimes: balanced, unidirectional skew, directional shift, sudden burst spike, overload. |
| **T** | Tuning & Reproducibility (參數與調整) | Staged roadmap (`Foundation Ready`, `Workflow Integration`, `Validation & Demo`); notes need for parameter sweep documentation. |
| **U** | Results & Counterexamples (初步結果) | Host Batch 1: `-18.28%` QVS (5/18 degraded); Host Batch 2: `-19.71%` QVS (2/6 degraded); Dev-Board: cycle-boundary activation & directional-shift improvement. |
| **V** | Validity & Limitations (有效性與限制) | Synthetic FIFO model ≠ real road; official minute-level data lacks continuous per-second dual-axis continuity. |

### Part 6: `V. Conclusion` (W–Z) & `References`

| Code | A–Z Element | Required Content in *Traffic Timing Assistant* |
| :--- | :--- | :--- |
| **W** | Restate Significance (重申意義) | **Fixes Proposal Gap W–Z:** Reaffirms explainable, verifiable edge AIoT control for isolated intersections. |
| **X** | Methodological Distinction (方法特色) | Compact decision tree + rule fallback + ARM/FPGA co-execution with deterministic cycle-boundary switching. |
| **Y** | Deliverables & Outcomes (成果交付) | Auditable decision logs, paired baseline benchmark, and hardware readback confirmation. |
| **Z** | Limitations & Future Work (限制與展望) | Root-cause ablation on the degraded cases (`5/18` and `2/6`), high-resolution per-second field logs, pedestrian/turning phases, sensor noise, multi-intersection coordination. |
| **Refs** | IEEE Bibliography | Complete `[1]`–`[6]` IEEE citations matching `第13組_Proposal.pdf`. |
