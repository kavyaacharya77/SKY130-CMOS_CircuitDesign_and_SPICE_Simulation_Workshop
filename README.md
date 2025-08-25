# CMOS Circuit Design and SPICE Simulation Workshop Using SKY130 Technology
## Brief Description of the Course
This repository contains my learning from the Cloud-based CMOS Circuit Design and SPICE Simulation Workshop, conducted by VLSI System Design (VSD) using an open-source SKY 130 PDK.         

This five-day workshop was designed to give a complete understanding of transistor-level behaviour and inverter design. The first day introduced about the MOSFET fundamentals through Id-Vds plots to study operating regions, while second day focused on velocity saturation and CMOS inverter basics, including Id-Vgs plots and threshold voltage extraction. The third day covered switvhing thresholds and dynamic simulations, relating (W/L) ratios to Vm and analysing delays. On the fourth day, noise margins amd robustness were explored by extracting NMH and NHL and studying their role in stable logic operation. The final day of this workshop dealt with power scling and process variations, showing how voltage and manufacturing changes affect inveter and chain performance. Overall, the workshop effectively combined theory with hands-on SPICE simulations to strengthen CMOS design fundamentals and practical skills.

# Index  

- [CMOS Circuit Design and SPICE Simulation Workshop Using SKY130 Technology](#cmos-circuit-design-and-spice-simulation-workshop-using-sky130-technology)  
  - [Brief Description of the Course](#brief-description-of-the-course)  

- [Day 1: Basics of NMOS Drain Current (Id) vs Drain-Source Voltage (Vds)](#day-1-basics-of-nmos-drain-current-id-vs-drain-to-source-voltage-vds)  
  - [Part 1: Introduction to Circuit Design and SPICE simulations](#part-1-introduction-to-circuit-design-and-spice-simulations)  
  - [Part 2: NMOS Resistive region and Saturation region of operation](#part-2-nmos-resistive-region-and-saturation-region-of-operation)  
  - [Part 3: Introduction to SPICE](#part-3-introduction-to-spice)  

- [Day 2: Velocity Saturation and basics of CMOS inverter VTC](#day-2-velocity-saturation-and-basics-of-cmos-inverter-vtc)  
  - [Part 1: SPICE simulation for lower nodes and velocity saturation effect](#part-1-spice-simulation-for-lower-nodes-and-velocity-saturation-effect)  
  - [Part 2: CMOS voltage transfer characteristics (VTC)](#part-2-cmos-voltage-transfer-characteristics-vtc)  

- [Day 3: CMOS switching threshold and dynamic simulations](#day-3-cmos-switching-threshold-and-dynamic-simulations)  
  - [Part 1: Voltage transfer characteristics and SPICE simulations](#part-1-voltage-transfer-characteristics-and-spice-simulations)  
  - [Part 2: Static Behavior Evaluation - CMOS Inverter Robustness: Switching threshold](#part-2-static-behavior-evaluation---cmos-inverter-robustness-switching-threshold)  

- [Day 4: CMOS Noise Margin Robustness Evaluation](#day-4-cmos-noise-margin-robustness-evaluation)  
  - [Part 1: Static Behavior Evaluation - CMOS Inverter Robustness: Noise Margin](#part-1-static-behavior-evaluation---cmos-inverter-robustness-noise-margin)  

- [Day 5: CMOS Power supply and device variation robustness evaluation](#day-5-cmos-power-supply-and-device-variation-robustness-evaluation)  
  - [Part 1: Static Behavior Evaluation - CMOS Inverter Robustness: Power Supply Variation](#part-1-static-behavior-evaluation---cmos-inverter-robustness-power-supply-variation)  
  - [Part 2: Static Behavior Evaluation - CMOS Inverter Robustness: Device Variation](#part-2-static-behavior-evaluation---cmos-inverter-robustness-device-variation)  

- [Conclusion](#conclusion)  
- [References](#references)  

# Day 1: Basics of NMOS Drain Current (Id) vs Drain-Source Voltage (Vds)
On the first day of the workshop, we were introduced to the fundamentals of MOSFET, its operartions and how to use SPICE for the circuit simulations. We began the session by revising the structure of an NMOS, its four terminals (Gate, Source, Drain and Body) and how different biasing conditions affect its operation. The concept of threshold voltage (Vt), stromg inversion and body effects were explained in detail, followed by derivations governing these parameters. Alongside theory, the basics of writing SPICE netlists and running simulations were also demonstrated.

# Part 1: Introduction to Circuit Design and SPICE simulations
### <ins>Key Learnings:
- Importance of (W/L) ratios in MOSFETs design.
- Need for SPICE simulations in circuit analysis.
- Structure and operation of NMOS transistor:
  - Four terminals → Gate (G), Source (S), Drain (D), Bulk/Body (B)
  - P-substrate with n+ diffusion regions
  - SiO₂ isolation layer, gate oxide, and poly-silicon/metal gate.

![WhatsApp Image 2025-08-25 at 20 55 48_bd066fc7](https://github.com/user-attachments/assets/398530b3-ea47-42ab-8d69-e10cd040fffa)

- Threshold Voltage (Vt):
The gate-to-source voltage (Vgs) at which strong inversion occurs.
- Strong Inversion:
When a part of the P-substrate inverts to form an N-type channel.
- Body Effect:
Applying a substrate bias (Vsb) increases the required threshold voltage.
- Threshold Voltage Equation:
  
  <img width="453" height="66" alt="image" src="https://github.com/user-attachments/assets/8b25ca41-d06e-40c2-b871-0faf19c692c7" />

where:
- *VT0* = Threshold voltage when 
- 𝑉𝑆𝐵=0
- 𝛾= Body effect coefficient (units: V^0.5)
- 𝜙𝑓 = Fermi potential
- *VSB* = Source-to-bulk voltage

- Body Effect:
  
  <img width="189" height="83" alt="image" src="https://github.com/user-attachments/assets/98330f1e-d733-4986-a250-b3f414f68fde" />

