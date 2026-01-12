---

# 🔋 Low-Power 8-Bit Carry Look-Ahead Adder Using Hybrid AND–XOR Logic and Unified AOI21 Carry Computation

![CMOS](https://img.shields.io/badge/CMOS-45nm-blue)
![Cadence](https://img.shields.io/badge/EDA-Cadence%20Virtuoso-orange)
![Adder](https://img.shields.io/badge/Arithmetic-CLA-green)
![Status](https://img.shields.io/badge/Status-Complete-success)
![License](https://img.shields.io/badge/License-MIT-lightgrey)

---

## 📌 Overview

This repository presents a **low-power 8-bit Carry Look-Ahead Adder (CLA)** designed in **45-nm CMOS** using **Cadence Virtuoso**.
The proposed design is built using a **hierarchical cascade of two optimized 4-bit CLA blocks**, where the **inter-block carry (C4)** is computed using a **fully factored AOI21-only formulation**.

Unlike conventional CLA implementations using AND–OR logic trees, this work employs:

* **Hybrid AND–XOR logic** for propagate/generate computation
* **Unified AOI21 logic** for all carry equations
* **Optimized C4 generation** to reduce inter-block carry delay

This approach achieves **significant power reduction** while maintaining competitive delay, making it suitable for low-power arithmetic units.

---

## 🧠 Design Motivation

### Why AOI21 for Carry Logic?

Carry computation dominates delay and power in CLA structures.
Through extensive evaluation, it was observed that:

* AND–OR based carry trees introduce:

  * higher logic depth
  * more internal nodes
  * increased switching activity
* AOI21 gates provide:

  * compact transistor realization
  * implicit inversion (reducing extra inverters)
  * lower parasitic capacitance

Hence, **all carry equations are mapped to AOI21 gates**, including the optimized inter-block carry **C4**.

---

## 🧮 Logic Equations (GitHub-Safe Format)

### Propagate, Generate, and Sum

```
Pi = Ai ⊕ Bi
Gi = Ai · Bi
Si = Pi ⊕ Ci
```

### Unified Carry Equation

```
C(n+1) = Gn + (Pn · Cn)
```

All carry equations are implemented using **AOI21 logic**.

---

## 🔬 Research Evolution (Step-by-Step)

### 1️⃣ Baseline 4-Bit CLA (Reference Implementation)

* Conventional carry look-ahead equations
* AND–OR based logic
* High switching activity

**Results:**

* Delay: ~63 ps
* Power: ~41.68 µW

---

### 2️⃣ Hybrid Logic 4-Bit CLA

* Hybrid AND and XOR gates for P/G generation
* AOI21 used for carry

**Results:**

* Delay: ~77.49 ps
* Power: ~11.13 µW

➡ ~73% power reduction with modest delay penalty.

---

### 3️⃣ Optimized C4 Carry Computation (Proposed 4-Bit CLA)

Instead of computing C4 through chained carry propagation, C4 is computed using a **fully factored AOI21 formulation** directly from P and G signals.

📌 **Reason for AOI21-only C4:**

* AOI21 implementation showed **lower delay and power** compared to AND–OR realization.
* Reduced logic depth for inter-block carry.

#### 📷 Optimized C4 Carry Logic

![C4 Optimized](C4_Optimized.png)

**Results (4-bit):**

* Delay: ~42.54 ps
* Power: ~16.94 µW

---

## 🧱 Hierarchical 8-Bit CLA Construction

### Why NOT Direct 8-Bit CLA?

A flat 8-bit CLA was implemented for comparison.

#### 📷 Direct 8-Bit CLA

![Direct 8-bit CLA](AOI21_CLA8-Bit.png)

**Results:**

* Delay: ~160.8 ps
* Power: ~44.49 µW
* Transistors: **200**

Although correct functionally, delay was high due to:

* Long carry logic fan-in
* Increased parasitics

---

### ✅ Proposed Solution: Cascaded 4-Bit CLA with Optimized C4

Two optimized 4-bit CLAs are cascaded, where:

* Lower block computes C0–C3
* **C4 is generated independently using AOI21**
* Upper block starts computation in parallel once C4 is available

#### 📷 Final Proposed 8-Bit CLA

![Proposed 8-bit CLA](proposed_8-Bit_CLA.png)

**Results (8-bit):**

* Delay: **~77 ps**
* Power: **~46 µW**
* PDP ≈ **3.54 fJ**
* Inter-block carry delay minimized

---

## 🔢 Transistor Count Analysis

### Proposed Optimized 4-Bit CLA

| Gate Type  | Transistors | Instances | Total   |
| ---------- | ----------- | --------- | ------- |
| AOI21      | 8           | 7         | 56      |
| Hybrid AND | 5           | 4         | 20      |
| Hybrid XOR | 6           | 8         | 48      |
| **Total**  | —           | —         | **124** |

---

### Direct 8-Bit CLA (Flat)

| Gate Type  | Transistors | Instances | Total   |
| ---------- | ----------- | --------- | ------- |
| AOI21      | 8           | 8         | 64      |
| Hybrid AND | 5           | 8         | 40      |
| Hybrid XOR | 6           | 16        | 96      |
| **Total**  | —           | —         | **200** |

➡ Despite higher transistor count in direct 8-bit CLA, **delay is significantly worse**, validating the hierarchical approach.

---

## 📈 Simulation Results

📌 **Waveforms and testbench simulations** will be uploaded here:

```
/simulation/
 ├── proposed_8bit_waveforms.pdf
 ├── testbench_8bit_cla.scs
 └── delay_power_summary.txt
```

(Repository will auto-update once files are added.)

---

## 🏆 Key Contributions

* Unified AOI21-based carry computation for all CLA stages
* Hybrid AND–XOR logic for low-power P/G generation
* Optimized C4 carry enabling parallel 4-bit block operation
* Demonstration that **hierarchical CLA outperforms flat CLA**
* Complete transistor-level design in 45-nm CMOS

---

## 🔮 Future Work

* Post-layout parasitic extraction (PEX)
* Extension to 16-bit and 32-bit CLA
* Integration into NCLA or Kogge-Stone hybrids
* Voltage scaling analysis

---

## 📜 License

MIT License — free to use for academic and research purposes.

---


