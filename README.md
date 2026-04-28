# Computational Modeling of Solid-Phase Extraction: Predicting Synthetic Urine Compound and Opioid Binding Behavior on the HyperSep Verify-Cx Sorbent

**Author:** Akilah Guthrie  
**Course:** CH374  
**Date:** April 28, 2026

---

## Table of Contents

1. [Project Overview](#project-overview)
2. [Computational Methods](#computational-methods)
3. [Key Findings](#key-findings)
4. [Limitations & Future Directions](#limitations--future-directions)
5. [File Structure](#file-structure)
6. [Navigation Instructions](#navigation-instructions)
7. [Prerequisites & Dependencies](#prerequisites--dependencies)

---

## Project Overview

This six-week computational research project investigated whether **density functional theory (DFT)-based molecular modeling** could serve as a predictive framework for understanding the solid-phase extraction (SPE) behavior of synthetic urine components and an opioid analyte.

The study examined the binding interactions of the following compounds with the **HyperSep Verify-Cx mixed-mode sorbent** — a commercially used SPE stationary phase relevant to forensic urine drug testing workflows:

- Urea
- Creatinine
- Hydrocodone

By computationally modeling these interactions, the project sought to improve mechanistic understanding of analyte retention and elution, with the broader goal of **reducing reliance on empirical trial-and-error** in SPE method development.

---

## Computational Methods

All calculations were performed using **ORCA**, a high-performance quantum chemistry software package.

**Level of Theory:** `B3LYP-D3BJ/def2-TZVP`

> A widely validated hybrid DFT method augmented with Grimme's D3 dispersion correction and Becke-Johnson damping, which improves the description of non-covalent interactions relevant to adsorption phenomena.

### Workflow

The modeling workflow proceeded in three stages:

1. **Monomer Optimization** — Individual monomers (urea, creatinine, and hydrocodone) and a truncated structural model of the Verify-Cx sorbent were constructed and optimized independently. Both protonated and unprotonated states of each analyte were considered.

2. **Complex Assembly** — Non-covalent complexes between each monomer and the sorbent model were assembled, with positional constraints applied to the sorbent to maintain structural integrity.

3. **Energy Extraction** — Geometry optimizations were performed on each complex, single-point energies were extracted from output log files, and binding energies were computed as:

    ΔE_binding = E_complex − (E_monomer + E_sorbent)

Key interatomic distances at the binding interface were also recorded to characterize interaction geometry.

---

## Key Findings

| Analyte | Binding Energy (relative) | Intermolecular Distance | Experimental SPE Behavior |
|---|---|---|---|
| Urea | More favorable | Longer | Removed in aqueous wash |
| Creatinine | More favorable | Longer | Removed in aqueous wash |
| Hydrocodone | Less favorable | **Shorter** | **Retained; elutes last** |

- Urea and creatinine exhibited **more favorable calculated binding energies** with the Verify-Cx sorbent model compared to hydrocodone.
- Hydrocodone demonstrated **shorter intermolecular binding distances**, suggesting closer geometric proximity to the sorbent's sulfonate interaction site (flanked by three oxygen atoms).
- These computational findings are **inconsistent** with experimentally observed SPE elution behavior, where hydrocodone is retained and elutes last.

---

## Limitations & Future Directions

### Current Limitations

- **Gas-phase modeling only** — No explicit solvent interactions; competitive solvation, aqueous matrix effects, and ionic strength are not captured.
- **Truncated sorbent model** — A molecular fragment rather than a full polymer network limits the model's ability to reproduce cooperative and steric effects.
- **No intermolecular analyte interactions** — Competitive retention effects between analytes were not modeled.

### Future Directions

- Incorporate explicit solvation models such as **CPCM** (conductor-like polarizable continuum model) or **QM/MM** hybrid methods.
- Expand the sorbent model to include a larger, more representative polymer fragment.
- Use **molecular dynamics (MD) simulations** to capture conformational flexibility and dynamic binding behavior over time.

---

## File Structure

    project-root/
    │
    ├── README.md                    ← You are here
    ├── project_banner.png           ← Title image for the research project
    │
    ├── XYZ_files/                   ← Molecular geometry files (.xyz)
    │   ├── Verify-CX/               ← Sorbent model geometries
    │   ├── Monomers/                ← Optimized monomer geometries (urea, creatinine, hydrocodone)
    │   └── Complexes/               ← Sorbent–analyte complex geometries
    │
    └── LOG_files/                   ← ORCA output log files
        ├── Verify-CX/               ← Sorbent optimization logs
        ├── Monomers/                ← Monomer optimization logs
        └── Complexes/               ← Complex optimization and energy logs

---

## Navigation Instructions

Follow this recommended order to understand the project from the ground up:

### Step 1 — Start with XYZ Files

XYZ files contain the 3D molecular geometries and are the best starting point for understanding the structures involved.

1. `XYZ_files/Verify-CX/` — Examine the sorbent model first to understand the stationary phase being studied.
2. `XYZ_files/Monomers/` — Review each analyte geometry (urea, creatinine, hydrocodone) in both protonated and unprotonated states.
3. `XYZ_files/Complexes/` — Examine the assembled sorbent–analyte complexes to see binding geometries.

### Step 2 — Review LOG Files

LOG files contain the full ORCA output, including energies, convergence data, and interatomic distances.

1. `LOG_files/Verify-CX/` — Sorbent optimization output.
2. `LOG_files/Monomers/` — Monomer optimization output and single-point energies.
3. `LOG_files/Complexes/` — Complex optimization output; use these to extract binding energies and intermolecular distances.

> **Tip:** Binding energies can be calculated by comparing the total energy in each complex log file against the corresponding monomer and sorbent log files.

---

## Prerequisites & Dependencies

### Software

| Tool | Purpose |
|---|---|
| [ORCA](https://www.faccts.de/orca/) | Quantum chemistry calculations (DFT) |
| [Avogadro](https://avogadro.cc/) or [GaussView](https://gaussian.com/gaussview6/) | Molecular structure visualization |
| [UCSF Chimera](https://www.cgl.ucsf.edu/chimera/) or [VMD](https://www.ks.uiuc.edu/Research/vmd/) | Optional: advanced visualization of complexes |

### Level of Theory

`B3LYP-D3BJ/def2-TZVP`

- **Functional:** B3LYP (hybrid DFT)
- **Dispersion correction:** Grimme's D3 with Becke-Johnson damping
- **Basis set:** def2-TZVP

### File Formats

- `.xyz` — Standard molecular geometry format, viewable in most molecular editors
- `.log` / `.out` — ORCA output files, readable as plain text

---

*This project was completed as part of CH374. For questions, contact Akilah Guthrie.*
