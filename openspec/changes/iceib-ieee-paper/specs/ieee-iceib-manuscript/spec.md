## ADDED Requirements

### Requirement: IEEE ICEIB Conference Layout Compliance
The manuscript in `ICEIB paper/main.txt` SHALL use the official IEEE conference document class (`\documentclass[conference]{IEEEtran}`) in double-column, 10-pt layout with IEEE keywords, numbered section headings, proper float captions (`\caption` + `\label`), and IEEE-formatted references ordered strictly by first appearance in the text, compatible with ICEIB (`https://www.iceib.asia/`).

#### Scenario: Standard IEEEtran LaTeX structure and citation ordering
- **WHEN** a user inspects or compiles `ICEIB paper/main.txt` as `main.tex` in Overleaf or `pdflatex`
- **THEN** the file uses `\documentclass[conference]{IEEEtran}`, `\begin{abstract}...\end{abstract}`, `\begin{IEEEkeywords}...\end{IEEEkeywords}`, properly captioned figures/algorithms, `\eqref` for equations, and `\begin{thebibliography}` ordered strictly by first citation appearance (`[1]` before `[2]`, etc.) without raw CJK characters in the body

### Requirement: Annotated Seven-Part Academic Section Structure
The manuscript and OpenSpec change artifacts SHALL organize and explicitly label the paper's seven core structural parts:
1. `Abstract` (`A`–`F`)
2. `I. Introduction` (`G`–`L`)
3. `II. Related Work` (`M`–`O`)
4. `III. Proposed Design` (`P` / `PA`–`PM`)
5. `IV. Experiment` (`Q`–`V`)
6. `V. Conclusion` (`W`–`Z`)
7. `References` (IEEE style)

#### Scenario: Section hierarchy verification
- **WHEN** all top-level headings in `ICEIB paper/main.txt`, `docs/ICEIB_Paper_A-Z.md`, and the per-section folders under `openspec/changes/iceib-ieee-paper/` (`abstract/`, `introduction/`, `related-work/`, `proposed-design/`, `experiment/`, `conclusion/`, `reference/`) are checked
- **THEN** the sequence is `Abstract`, `I. Introduction`, `II. Related Work`, `III. Proposed Design`, `IV. Experiment`, `V. Conclusion`, and `References`

### Requirement: Complete Traceability and Empirical Honesty
All cited references, system modules, pseudocode steps, and preliminary quantitative results in the manuscript SHALL match `第13組_Proposal.pdf` and `docs/交通專題分析_A-Z.md`, explicitly disclosing degraded cases (`5 of 18` and `2 of 6` without pooling across separate test batches) and synthetic FIFO limitations without fabricating unverified road metrics or institutional names.

#### Scenario: Preliminary results and limitation disclosure
- **WHEN** `IV. Experiment` and `V. Conclusion` present quantitative findings
- **THEN** they report the 18-scenario batch (-18.28% QVS, 5 degraded), 6-scenario batch (-19.71% QVS, 2 degraded) independently, dev-board cycle-boundary readback test, and explicitly note FIFO simulation and minute-level official data limitations
