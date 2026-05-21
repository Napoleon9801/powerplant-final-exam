# PowerPlant Engineering — Final Exam Study Guide

**SUT EE · 2026 · Chinnawat Dumklang**

> Comprehensive exam preparation for PowerPlant Engineering (โรงไฟฟ้า) final exam.
> Covers all 6 written questions (30 pts) with full worked examples sourced directly from lecture slides.

## Live Site

**[napoleon9801.github.io/powerplant-final-exam/PowerPlant_Final_Exam_Complete.html](https://napoleon9801.github.io/powerplant-final-exam/PowerPlant_Final_Exam_Complete.html)**

## What's Inside

| File | Description |
|------|-------------|
| `PowerPlant_Final_Exam_Complete.html` | Main study guide — all 6 written questions, MathJax equations, worked examples, warnings |
| `Final_Exam_Guide.md` | Exam question breakdown, formulas cheat sheet |
| `Final_Exam_Cheatsheet.html` | Quick-reference cheatsheet |
| `chapter6/` – `chapter10/` | Lecture slide images (PNG) per chapter |

## Topics Covered

| # | Chapter | Topic |
|---|---------|-------|
| Q1 | Ch6 | **Economic Load Dispatch** — Priority List, Priority Index σ, Unit Commitment Table, Lambda Iteration |
| Q2 | Ch7 | **AGC Multi-Area** — ACE formula, 2-area & 3-area tie-line balance |
| Q3 | Ch8 | **Bus Arrangement** — 7 types (SBSB, DBDB, MATB, DMAST, DBSB, Ring Bus, BAAH) |
| Q4 | Ch8 | **Touch & Step Voltage** — IEEE 80, derating factor Cs, 3 surface material cases |
| Q5 | Ch8 | **Ground Grid Resistance** — Sverak formula, L_T counting from grid diagram |
| Q6 | Ch10 | **Relay Setting (IDMT)** — IEC 60255, 4 curve types, 5-step method, protection coordination |

## Exam Format

- **Total:** 50 points
- **Section A:** 60 multiple choice → 20 pts
- **Section B:** 6 written questions × 5 pts = 30 pts

## Key Formulas at a Glance

**Priority Index**
$$\sigma_i = \frac{F_i(P_{i,\max})}{P_{i,\max}} \quad [\text{฿/MWh}]$$

**Area Control Error**
$$\text{ACE}_i = \Delta P_{\text{tie},i} + B_i \cdot \Delta f$$

**Touch & Step Voltage (IEEE 80)**
$$E_{\text{touch}} = (1000 + 1.5 \cdot C_s \cdot \rho_s) \cdot \frac{0.116}{\sqrt{t_s}}$$

**Sverak Ground Grid Resistance**
$$R_G = \rho_E \left[\frac{1}{L_T} + \frac{1}{\sqrt{20A}}\left(1 + \frac{1}{1 + h\sqrt{20/A}}\right)\right]$$

**IDMT Operating Time (Standard Inverse)**
$$T = \text{TMS} \times \frac{0.14}{\text{PSM}^{0.02} - 1}$$
