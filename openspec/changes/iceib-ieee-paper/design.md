## Context

The repository (`czk001167-hash/AIOT-DIC4`) contains Group 13's *Traffic Timing Assistant* proposal (`第13組_Proposal.pdf`), an A–Z SOP compliance analysis (`docs/交通專題分析.pdf`, `docs/交通專題分析_A-Z.md`, `assets/A-Z分析.png`), a project overview (`README.md`), A–Z academic guides (`docs/ICEIB_A-Z_Writing_Guide.md`, `docs/ICEIB_Paper_A-Z.md`), and the IEEE conference draft (`ICEIB paper/main.txt`).

The user's goal is to manage academic paper authoring through OpenSpec so that:
1. The paper targets **ICEIB** (`https://www.iceib.asia/`) in standard IEEE double-column conference format (`IEEEtran`).
2. The paper strictly follows the seven labeled structural sections:
   - **Abstract** (`A`–`F`)
   - **I. Introduction** (`G`–`L`)
   - **II. Related Work** (`M`–`O`)
   - **III. Proposed Design** (`P` / `PA`–`PM`)
   - **IV. Experiment** (`Q`–`V`)
   - **V. Conclusion** (`W`–`Z`)
   - **References** (IEEE numbered bibliography)
3. The writing follows the **2020 A–Z SOP academic writing framework** (`A`–`Z`) documented in `docs/`, closing the two structural gaps previously identified in `docs/交通專題分析_A-Z.md` (missing Introduction organization `L` and missing standalone Conclusion `W–Z`).

## Annotated Paper Section Map (A–Z Alignment)

| Paper Section Heading | LaTeX / Markdown Anchor | A–Z Coverage | Current Status & Key Audit Notes |
| :--- | :--- | :--- | :--- |
| **Abstract** | `\begin{abstract}` (`main.txt` L56–69) | `A`–`F` | Structure complete (~178 words); expand `AIoT` on first use and mention balanced/burst causes of degraded cases in `F`. |
| **I. Introduction** | `\section{Introduction}` (`main.txt` L78–103) | `G`–`L` | Includes gap `L` organization; **fix IEEE citation order** (currently `[4], [5]` appear before `[1]`) and ground or remove un-cited corridor sentence. |
| **II. Related Work** | `\section{Related Work}` (`main.txt` L108–144) | `M`–`O` | Balanced 3 AI + 3 Traffic sources with 8-column `Table I`; reduce prose repetition with Section I and align `[1]`–`[6]` order. |
| **III. Proposed Design** | `\section{Proposed Design}` (`main.txt` L149–237) | `P` (`PA`–`PM`) | **Fix `\label{alg:control_loop}` inside `figure` without `\caption`** (use `algorithm` environment); add Architecture (`Fig. 1`) & Flowchart (`Fig. 2`) visuals plus explicit plan durations/thresholds and queue-service equation. |
| **IV. Experiment** | `\section{Experiment}` (`main.txt` L242–288) | `Q`–`V` | Use `\label{eq:qvs}` / `\eqref{eq:qvs}`; add synthetic scenario parameter table and breakdown of degraded cases (5/18, 2/6); add quantitative board metrics; replace proposal roadmap `Table III` with experimental parameters. |
| **V. Conclusion** | `\section{Conclusion}` (`main.txt` L293–310) | `W`–`Z` | Standalone conclusion present; revise `"7 combined degraded scenarios"` wording to keep batches separate (`5 of 18` and `2 of 6`). |
| **References** | `\begin{thebibliography}` (`main.txt` L315–335) | IEEE Style | Re-order `[1]`–`[6]` to match first appearance in Section I; add access dates for online/news references. |

## Goals / Non-Goals

**Goals:**
- Map every stage of the 2020 A–Z SOP framework (`A`–`Z`) explicitly onto the seven IEEE ICEIB conference paper sections (`Abstract`, `I. Introduction`, `II. Related Work`, `III. Proposed Design`, `IV. Experiment`, `V. Conclusion`, `References`).
- Store the A–Z style guide (`docs/ICEIB_A-Z_Writing_Guide.md`) and full A–Z structured manuscript (`docs/ICEIB_Paper_A-Z.md`) in `docs/`.
- Maintain `ICEIB paper/main.txt` in `pdflatex`-safe `IEEEtran` LaTeX syntax and track section-by-section revisions cleanly inside `openspec/changes/iceib-ieee-paper/`.
- Preserve strict empirical honesty: report only observed synthetic FIFO results (including degraded cases: 5/18 and 2/6) and dev-board activation tests without fabricating unverified road metrics or institutional metadata.

**Non-Goals:**
- Compiling the LaTeX file to PDF locally (`pdflatex` is not installed in the workspace environment; compilation is left for Overleaf or a TeX Live environment).
- Modifying or deleting the original source proposal (`第13組_Proposal.pdf`) or original reviewer analysis (`docs/交通專題分析_A-Z.md`).
- Inventing unverified author romanizations, university affiliations, or live road experiments.

## Decisions

- **Decision 1: Consolidate Deep Research (M1–M5, C1–C3, Q1–Q10) inside Section III (Proposed Design).**
  - *Rationale:* The user explicitly specified seven top-level parts (`Abstract`, `Introduction`, `Related Work`, `Proposed Design`, `Experiment`, `Conclusion`, `References`). Placing the five design mindsets and three architectural trade-offs as `III-A Design Rationale and Trade-offs` directly connects domain research to the eight-module ARM/FPGA architecture (`III-B`), workflow/algorithm (`III-C`), and case/queue formulation (`III-D`, covering `PA–PM`).
- **Decision 2: Maintain dual synchronized deliverables (`docs/` Markdown A–Z artifacts + `ICEIB paper/main.txt` IEEEtran LaTeX).**
  - *Rationale:* `docs/ICEIB_A-Z_Writing_Guide.md` and `docs/ICEIB_Paper_A-Z.md` serve human review and A–Z traceability in `docs/`, while `ICEIB paper/main.txt` provides ready-to-compile IEEEtran LaTeX for ICEIB (`https://www.iceib.asia/`).
- **Decision 3: Keep `pdflatex`-safe ASCII LaTeX with bracketed author/affiliation placeholders.**
  - *Rationale:* Raw CJK characters break standard `IEEEtran` `pdflatex` compilation without `CJKutf8`/`xeCJK`, and institutional affiliation/official passport romanizations are not present in the source PDFs.

## Risks / Trade-offs

- **Local TeX verification gap** → Mitigated by auditing LaTeX syntax, `\label`/`\ref` targets, citation ordering, and table column widths (`< 18.19 cm` for `table*`, `< 8.89 cm` for `table`), with final build in Overleaf (`main.tex`).
- **Placeholder author metadata** → Mitigated by marking `[Qi-Rui Wu]`, `[Po-Sheng Wei]`, `[Jen-Kai Chen]`, `[Department Name]`, `[University Name]` clearly with `%` comments containing the exact Chinese names and student IDs from `第13組_Proposal.pdf`.
- **ICEIB cycle-specific template variations** → Mitigated by verifying active cycle page size (Letter vs. A4), page limit (4–6 pages), and blind-review rules on `https://www.iceib.asia/`.
