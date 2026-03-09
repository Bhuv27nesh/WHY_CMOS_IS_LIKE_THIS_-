# CMOS vs Reversed CMOS – Simulation and Analysis

## Overview

Complementary Metal Oxide Semiconductor (CMOS) is the most widely used technology for digital integrated circuits.  
In CMOS logic, **PMOS transistors form the pull-up network (PUN)** and **NMOS transistors form the pull-down network (PDN)**.

This repository demonstrates:

- The working of a **standard CMOS inverter**
- The behavior when the **CMOS structure is reversed**
- Simulation results comparing both structures
- Concepts of **strong and weak logic levels**

The simulations were performed using a transient analysis with a **1.8V supply**.

---

# CMOS Logic

CMOS stands for **Complementary MOS**, meaning it uses both:

- **PMOS transistors**
- **NMOS transistors**

These transistors are arranged in a complementary way so that **only one network conducts at a time**, minimizing static power consumption.

Typical CMOS inverter structure:  
<img width="552" height="277" alt="regu_cmos" src="https://github.com/user-attachments/assets/56ad9bb5-5b5b-4d42-b2a0-634b9ec15d58" />


Input is connected to **both transistor gates**.

| Input | PMOS | NMOS | Output |
|------|------|------|-------|
| 0 | ON | OFF | 1 |
| 1 | OFF | ON | 0 |

This results in:

- Full voltage swing
- Very low static power
- High noise margin

---

# Strong and Weak Logic Levels

MOS transistors do not pass both logic levels equally well.

This leads to the concepts of **strong and weak logic levels**.

## Strong Logic

A **strong logic level** means the transistor can pass the voltage level completely.

| Transistor | Strong Logic |
|-------------|-------------|
| NMOS | Strong 0 |
| PMOS | Strong 1 |

### NMOS

NMOS passes **strong logic 0**.

When pulling the output to ground:  
Vout ≈ 0V


But NMOS cannot pass a full logic 1.  
Output becomes:

Vout = VDD - VTN

This is called a **weak 1**.

---

### PMOS

PMOS passes **strong logic 1**.

When pulling the output to VDD:
Vout ≈ VDD


But PMOS cannot pass a full logic 0.  
Output becomes:
Vout ≈ |VTP|


This is called a **weak 0**.

---

# Summary of Strong and Weak Logic

| Transistor | Strong | Weak |
|-------------|-------|------|
| NMOS | Strong 0 | Weak 1 |
| PMOS | Strong 1 | Weak 0 |

This property is the **main reason CMOS uses PMOS for pull-up and NMOS for pull-down**.

---

# Why CMOS Uses PMOS Pull-Up and NMOS Pull-Down

Correct CMOS arrangement:

- **PMOS → Pull-up network**
- **NMOS → Pull-down network**

Reasons:

1. PMOS provides **strong logic 1**
2. NMOS provides **strong logic 0**
3. Full voltage swing is achieved
4. High noise margin
5. Minimal static power consumption

This ensures reliable digital switching.

---

# What Happens If CMOS is Reversed

If we reverse the structure:

- **NMOS used as pull-up**
- **PMOS used as pull-down**

Structure becomes:  
<img width="550" height="273" alt="rev_cmos" src="https://github.com/user-attachments/assets/60e5116d-5bca-43ea-91eb-23fe741cf077" />

This configuration causes several problems.

## 1. NMOS Cannot Pull Output Fully to VDD

NMOS stops conducting when:
VGS = VTN

So the output becomes:
Vout = VDD - VTN

For example:
Vout ≈ 0.9V


This results in a **weak logic 1**.

---

## 2. PMOS Cannot Pull Output Fully to GND

PMOS stops when:

VSG = |VTP|

So output becomes approximately:
Vout ≈ |VTP|


Which is **not a full 0V**.

This creates a **weak logic 0**.

---

## 3. Output Stuck Near Mid-Level

Because neither transistor can fully drive the output:

- NMOS cannot reach VDD
- PMOS cannot reach GND

The output often stabilizes near:
VDD / 2


This creates an **analog voltage instead of digital logic**.

---

## 4. Reduced Noise Margin

Digital circuits require clear logic levels.

But reversed CMOS produces:

| Intended | Actual |
|--------|--------|
| Logic 1 | VDD - VTN |
| Logic 0 | VTP |

This reduces **noise immunity** and causes unreliable operation.

---

# Simulation Performed

To demonstrate this behavior, two circuits were simulated:

1. **Regular CMOS inverter**
2. **Reversed CMOS structure**

Simulation parameters:

- Supply voltage: **1.8 V**
- Input signal: **Pulse waveform**
- Transient analysis performed
- Load capacitor included at the output

---

# Simulation Results  

<img width="1018" height="752" alt="WHY_CMOS_WHY" src="https://github.com/user-attachments/assets/97bbeae5-02e3-4d29-be2f-54a990f090d0" />

## Regular CMOS

Observed behavior:

- Output is the **perfect inversion of input**
- Full voltage swing between **0 V and 1.8 V**
- Proper digital switching

This confirms the correct CMOS operation.

---

## Reversed CMOS

Observed behavior:

- Output remains around **0.9 V**
- Output does **not switch properly**
- Voltage settles near **mid-level**

This happens because:
Vout ≈ VDD - VTN


Since NMOS cannot pull the output fully to VDD and PMOS cannot pull it fully to GND.

---

# Key Takeaways

- NMOS passes **strong 0 but weak 1**
- PMOS passes **strong 1 but weak 0**
- CMOS uses **PMOS pull-up and NMOS pull-down** to achieve full logic levels
- Reversing the structure leads to **degraded output and improper switching**

The simulation clearly demonstrates why **standard CMOS architecture is necessary for reliable digital logic**.

---
