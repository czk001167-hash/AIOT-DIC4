## 0. A-to-Z Academic Writing Foundation (`docs/` & OpenSpec)

- [x] 0.1 Create `docs/ICEIB_A-Z_Writing_Guide.md` defining the 2020 A–Z SOP writing framework (`A`–`Z` and `PA`–`PM`) mapped onto the seven ICEIB paper sections.
- [x] 0.2 Create `docs/ICEIB_Paper_A-Z.md` containing the complete A–Z tagged English manuscript draft (`[A]`–`[Z]`).
- [x] 0.3 Document section-by-section change logs in dedicated per-section folders (`abstract/`, `introduction/`, `related-work/`, `proposed-design/`, `experiment/`, `conclusion/`, `reference/`).

## 1. Abstract (`A`–`F`)

- [x] 1.1 Draft complete six-step `Abstract` (`A`–`F`) + `IEEEkeywords` in `ICEIB paper/main.txt` and `docs/ICEIB_Paper_A-Z.md`.
- [x] 1.2 Expand `AIoT` on first occurrence and note in `[F]` that degraded cases concentrate in balanced and burst-demand regimes.
- [ ] 1.3 Replace bracketed author/affiliation/email placeholders in `\author{...}` (or anonymize if active ICEIB track is double-blind).

## 2. I. Introduction (`G`–`L`)

- [x] 2.1 Draft `I. Introduction` covering `G`–`K` and add the missing paper organization paragraph (`L`).
- [x] 2.2 Fix IEEE citation numbering order so references cited first in `I. Introduction` appear as `[1], [2], ...` in sequence.
- [x] 2.3 Merge the uncited corridor field-trial sentence in `[G]` cleanly into the verified `[1], [2]` references.

## 3. II. Related Work (`M`–`O`)

- [x] 3.1 Draft `II. Related Work` with 3 AI + 3 Traffic sources (`M`–`N`), 8-column `Table I`, and Research Gap positioning (`O`).
- [x] 3.2 Tighten repetitive listing of the 6 references between `I. Introduction` and `Table I` and align `[1]`–`[6]` numbering.

## 4. III. Proposed Design (`P` / `PA`–`PM`)

- [x] 4.1 Draft `III. Proposed Design` covering Design Rationale (`M1`–`M5`, `C1`–`C3`), 8-module ARM/FPGA loop, 12-line `Algorithm 1`, and QVS equation.
- [x] 4.2 Fix `Algorithm 1` LaTeX float/label bug (switch to `\usepackage{algorithm}` + `\caption` before `\label{alg:control_loop}`).
- [x] 4.3 Add self-contained TikZ vector figures for the 8-module System Architecture (`Fig. 1`) and Processing Flowchart (`Fig. 2`).
- [x] 4.4 Add discrete-time FIFO queue update equation $q_d(t+1)=\max(0, q_d(t)+a_d(t)-s_d(t))$ in `III-D`.
- [ ] 4.5 Populate concrete timing plan durations ($G_{\min}$, $G_{\max}$, cycle length) and decision-tree depth/thresholds once exported from prototype config.

## 5. IV. Experiment (`Q`–`V`)

- [x] 5.1 Draft `IV. Experiment` covering metrics (`Q`), baseline (`R`), synthetic scenarios (`S`), preliminary paired & board results (`U`), and validity scope (`V`).
- [x] 5.2 Add `\label{eq:qvs}` to Equation `(2)` and reference equations via `\eqref{eq:queue_update}` and `\eqref{eq:qvs}`.
- [x] 5.3 Replace proposal roadmap `Table III` with `Table II` (`tab:scenarios`) summarizing the 5 synthetic evaluation regimes.
- [ ] 5.4 Populate per-scenario parameter values ($\lambda$, $\mu$, $T$, seeds), per-case breakdown of the `5/18` and `2/6` degraded cases, and measured board ms latencies.

## 6. V. Conclusion (`W`–`Z`)

- [x] 6.1 Draft standalone `V. Conclusion` (`W`–`Z`) resolving the missing conclusion gap identified in `docs/交通專題分析_A-Z.md`.
- [x] 6.2 Revise `"7 combined degraded scenarios"` to `"the degraded cases observed in both host test batches (5 of 18 and 2 of 6)"` to avoid pooling independent batches.

## 7. References (IEEE Style)

- [x] 7.1 Format all 6 citations from `第13組_Proposal.pdf` in IEEE `\begin{thebibliography}` style.
- [x] 7.2 Re-order `\bibitem` entries strictly by first citation appearance in `I. Introduction` (`[1]`–`[6]`).

## 8. Validation & Compilation

- [x] 8.1 Run `openspec validate iceib-ieee-paper` and `openspec status --change "iceib-ieee-paper"`.
- [ ] 8.2 Rename `ICEIB paper/main.txt` to `main.tex` and compile in Overleaf / `pdflatex` to verify 4–6 page ICEIB limit, TikZ figures, and zero LaTeX warnings.
