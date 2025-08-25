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
