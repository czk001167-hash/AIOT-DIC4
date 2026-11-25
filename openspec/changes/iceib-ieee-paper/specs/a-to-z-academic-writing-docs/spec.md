## ADDED Requirements

### Requirement: A-to-Z SOP Writing Specification in Docs
The repository SHALL include an explicit 2020 A–Z SOP academic writing guide in `docs/ICEIB_A-Z_Writing_Guide.md` mapping every element `A` through `Z` onto the ICEIB IEEE conference paper sections (`Abstract`: A–F, `Introduction`: G–L, `Related Work`: M–O, `Proposed Design`: P/PA–PM, `Experiment`: Q–V, `Conclusion`: W–Z).

#### Scenario: Complete A-to-Z mapping coverage
- **WHEN** a reader inspects `docs/ICEIB_A-Z_Writing_Guide.md`
- **THEN** every code from `A` to `Z` (plus `PA`–`PM`) is explicitly defined, mapped to an IEEE paper section, and cross-referenced against Group 13's proposal content and previously identified gaps (`L` and `W–Z`)

### Requirement: A-to-Z Annotated ICEIB Paper Draft in Docs
The repository SHALL include a complete A–Z annotated English paper draft in `docs/ICEIB_Paper_A-Z.md` mirroring `ICEIB paper/main.txt` so that every paragraph and subsection is visibly tagged with its corresponding A–Z stage (`[A]`–`[Z]`).

#### Scenario: A-to-Z tagged paper draft in docs
- **WHEN** a reader inspects `docs/ICEIB_Paper_A-Z.md`
- **THEN** all six required sections (`Abstract`, `I. Introduction`, `II. Related Work`, `III. Proposed Design`, `IV. Experiment`, `V. Conclusion`, and `References`) are present with explicit `[A]`–`[Z]` tags and all six proposal references (`[1]`–`[6]`)
