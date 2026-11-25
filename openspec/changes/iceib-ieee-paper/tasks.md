## 0. A-to-Z Academic Writing Foundation (`docs/` & OpenSpec)

- [x] 0.1 Create `docs/ICEIB_A-Z_Writing_Guide.md` defining the 2020 A–Z SOP writing framework (`A`–`Z` and `PA`–`PM`) mapped onto the seven ICEIB paper sections.
- [x] 0.2 Create `docs/ICEIB_Paper_A-Z.md` containing the complete A–Z tagged English manuscript draft (`[A]`–`[Z]`).
- [x] 0.3 Document section-by-section change logs in dedicated per-section folders (`abstract/`, `introduction/`, `related-work/`, `proposed-design/`, `experiment/`, `conclusion/`, `reference/`).

## 1. Abstract (`A`–`F`)

- [x] 1.1 Draft complete six-step `Abstract` (`A`–`F`) + `IEEEkeywords` in `ICEIB paper/main.txt` and `docs/ICEIB_Paper_A-Z.md`.
- [ ] 1.2 Expand `AIoT` on first occurrence and briefly note in `[F]` that degraded cases concentrate in balanced and burst-demand regimes.
- [ ] 1.3 Replace bracketed author/affiliation/email placeholders in `\author{...}` (or anonymize if active ICEIB track is double-blind).

## 2. I. Introduction (`G`–`L`)

- [x] 2.1 Draft `I. Introduction` covering `G`–`K` and add the missing paper organization paragraph (`L`).
- [ ] 2.2 Fix IEEE citation numbering order so references cited first in `I. Introduction` appear as `[1], [2], ...` in sequence rather than `[4], [5]` before `[1]`.
- [ ] 2.3 Cite an explicit verifiable reference for the corridor field-trial sentence in `[G]` or merge it cleanly into `[4], [5]`.

## 3. II. Related Work (`M`–`O`)

- [x] 3.1 Draft `II. Related Work` with 3 AI + 3 Traffic sources (`M`–`N`), 8-column `Table I`, and Research Gap positioning (`O`).
- [ ] 3.2 Tighten repetitive listing of the 6 references between `I. Introduction` and `Table I` to emphasize comparative insights.

## 4. III. Proposed Design (`P` / `PA`–`PM`)

- [x] 4.1 Draft `III. Proposed Design` covering Design Rationale (`M1`–`M5`, `C1`–`C3`), 8-module ARM/FPGA loop, 12-line `Algorithm 1`, and QVS equation.
- [ ] 4.2 Fix `Algorithm 1` LaTeX float/label bug (`main.txt` L187–225: switch from uncaptioned `figure` to `\usepackage{algorithm}` + `\caption` before `\label{alg:control_loop}`).
- [ ] 4.3 Add vector/high-DPI figures for the 8-module System Architecture (`Fig. 1`) and Processing Flowchart (`Fig. 2`) adapted from `第13組_Proposal.pdf`.
- [ ] 4.4 Specify concrete timing plan parameters (green/yellow/all-red durations, $G_{\min}$, $G_{\max}$), decision-tree depth/thresholds, and queue-service update equation $q(t+1)=\max(0, q(t)+a(t)-s(t))$.

## 5. IV. Experiment (`Q`–`V`)

- [x] 5.1 Draft `IV. Experiment` covering metrics (`Q`), baseline (`R`), synthetic scenarios (`S`), staged roadmap (`T`), preliminary paired & board results (`U`), and validity scope (`V`).
- [ ] 5.2 Add `\label{eq:qvs}` to Equation `(1)` and reference it via `\eqref{eq:qvs}` in `IV-A`.
- [ ] 5.3 Add a synthetic scenario & parameter table ($\lambda$, $\mu$, duration $T$, seeds) and break down which regimes caused the `5/18` and `2/6` degraded cases.
- [ ] 5.4 Add quantitative hardware measurements (inference/readback latency, board QVS delta) to `Dev-Board Paired Test`, and replace proposal-style `Table III` (work roadmap) with an experiment configuration or ablation table.

## 6. V. Conclusion (`W`–`Z`)

- [x] 6.1 Draft standalone `V. Conclusion` (`W`–`Z`) resolving the missing conclusion gap identified in `docs/交通專題分析_A-Z.md`.
- [ ] 6.2 Revise `"7 combined degraded scenarios"` (`main.txt` L307) to `"the degraded cases observed in both host batches (5 of 18 and 2 of 6)"` to avoid pooling independent batches.

## 7. References (IEEE Style)

- [x] 7.1 Format all 6 citations from `第13組_Proposal.pdf` in IEEE `\begin{thebibliography}` style.
- [ ] 7.2 Re-order `\bibitem` entries strictly by first citation appearance in `I. Introduction` and add `[Online]` access dates for web/news citations.

## 8. Validation & Compilation

- [x] 8.1 Run `openspec validate iceib-ieee-paper` and `openspec status --change "iceib-ieee-paper"`.
- [ ] 8.2 Rename `ICEIB paper/main.txt` to `main.tex` and compile in Overleaf / `pdflatex` to verify 4–6 page ICEIB limit, table fit, and zero LaTeX warnings.
