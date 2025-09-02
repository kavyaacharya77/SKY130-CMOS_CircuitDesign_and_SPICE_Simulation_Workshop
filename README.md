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
On the first day of the workshop, we were introduced to the fundamentals of MOSFET, its operartions and how to use SPICE for the circuit simulations. We began the session by revising the structure of an NMOS, its four terminals (Gate, Source, Drain and Body/Bulk) and how different biasing conditions affect its operation. The concept of threshold voltage (Vt), stromg inversion and body effects were explained in detail, followed by derivations governing these parameters. Alongside theory, the basics of writing SPICE netlists and running simulations were also demonstrated.

# Part 1: Introduction to Circuit Design and SPICE simulations
### <ins>Key Learnings:
- Importance of (W/L) ratios in MOSFETs design.
- Need for SPICE simulations in circuit analysis.
- Structure and operation of NMOS transistor:
  - Four terminals → Gate (G), Source (S), Drain (D), Bulk/Body (B)
  - P-substrate with n+ diffusion regions
  - SiO₂ isolation layer, gate oxide, and poly-silicon/metal gate.

![WhatsApp Image 2025-08-25 at 20 55 48_bd066fc7](https://github.com/user-attachments/assets/398530b3-ea47-42ab-8d69-e10cd040fffa)

Figure 1: Structure of NMOS Transistor

- Threshold Voltage (Vt):
The gate-to-source voltage (Vgs) at which strong inversion occurs.
- Strong Inversion:
When a part of the P-substrate inverts to form an N-type channel.
- Body Effect:
Applying a substrate bias (Vsb) increases the required threshold voltage.

### Threshold Voltage Equation:
  
  <img width="453" height="66" alt="image" src="https://github.com/user-attachments/assets/8b25ca41-d06e-40c2-b871-0faf19c692c7" />

where:
- *VT0* = Threshold voltage when 
- 𝑉𝑆𝐵=0
- 𝛾= Body effect coefficient (units: V^0.5)
- 𝜙𝑓 = Fermi potential
- *VSB* = Source-to-bulk voltage

### Body Effect Coefficient
  
  <img width="189" height="83" alt="image" src="https://github.com/user-attachments/assets/98330f1e-d733-4986-a250-b3f414f68fde" />

where:
- 𝜀𝑠𝑖​ = Permittivity of silicon (=11.7ε0)
- 𝑁𝐴 = Substrate doping concentration
- *q* = Electronic charge (1.6×10^−19 𝐶)
- 𝐶𝑜𝑥 = Oxide capacitance per unit area

### Fermi Potential Equation

<img width="242" height="47" alt="image" src="https://github.com/user-attachments/assets/b84ae6d3-4ebb-4b84-ae28-cb574b328352" />

where:
- 𝑘 = Boltzmann constant
- 𝑇 = Absolute temperature (K)
- 𝑛𝑖 = Intrinsic carrier concentration of silicon

# Part 2: NMOS Resistive region and Saturation region of operation
### <ins>Key Learnings:
- The Resistive Region is also known as the Linear Region of MOSFET operation.
- At threshold: VGS=VT. When VGS>VT, a channel forms, and induced charge depends on (VGS−VT).
- For analysis:
  - Assume 𝑉𝐺𝑆=1𝑉GS=1V, 𝑉𝑇=0.45
  - At 𝑉𝐷𝑆≈0, channel voltage is constant. With finite 𝑉𝐷𝑆, voltage varies along channel length 𝐿.
    
Let:
- 𝑉(𝑥) = channel potential at distance 𝑥 along channel length
- 𝑉𝐺𝑆−𝑉(𝑥) = gate-to-channel voltage at that point

Thus, induced charge at point 𝑥:

<img width="338" height="34" alt="image" src="https://github.com/user-attachments/assets/5b19be93-2451-423d-bab4-87ebdc3e9d94" />

### Gate oxide capacitance:

<img width="123" height="65" alt="image" src="https://github.com/user-attachments/assets/098ca971-a21b-42c1-bf87-4f175296ffb7" />

where:
- *εox*​ = 3.97ε0​=3.51×10−11F/m
- *tox* = oxide thickness

### Types of Current
- Drift Current → due to potential difference
- Diffusion Current → due to carrier concentration gradient
- For MOSFETs, current is mostly drift dominated.

### Drift Current

<img width="360" height="65" alt="image" src="https://github.com/user-attachments/assets/d8d5ab17-dab7-405c-8f6b-a47f2c5c97ed" />

where:
- *μn* = electron mobility
- *W* = channel width
- *L* = channel length
- *kn′* = *μn​Cox* = process transconductance
- 𝑘𝑛 = 𝑘𝑛′⋅𝑊/𝐿 = gain factor

### Region Conditions
- Linear / Resistive Region: 𝑉𝐷𝑆 ≤ (𝑉𝐺S−𝑉𝑇)
  
  Approximate current: 𝐼𝐷 ≈ 𝑘𝑛(𝑉𝐺𝑆−𝑉𝑇)𝑉𝐷𝑆

- Saturation (Pinch-off) Region:
When: 𝑉𝐷𝑆 ≥ (𝑉𝐺𝑆−𝑉𝑇)
Pinch-off occurs near the drain; channel shape becomes triangular. Current is given by: 𝐼𝐷𝑠𝑎𝑡 = 1/2𝑘𝑛(𝑉𝐺𝑆−𝑉𝑇)^2ID

### With Channel Length Modulation
In reality, the drain current still slightly increases with 𝑉𝐷S because the effective channel length decreases when 𝑉𝐷𝑆 increases (pinch-off moves closer to the source). 

In this case, the Drain current ID equation becomes:

<img width="277" height="61" alt="image" src="https://github.com/user-attachments/assets/4684ddd9-aa90-4003-bc67-6b533c984a43" />

This effect is modeled by multiplying with the factor: (1+𝜆𝑉𝐷𝑆).

where:
- *λ* = channel-length modulation parameter (units: 𝑉^−1)
- Larger 𝜆 = stronger dependence of ID on VDS.
- For long-channel MOSFETs, λ≈0 → current almost flat​.
- For short-channel devices, 𝜆 is significant.

# Part 3: Introduction to SPICE
### <ins>Key Learnings:
- SPICE Waveforms: Can be used to calculate the delay of a cell. These delays are very close to real/practical delays.
- SPICE Model Parameters: Define device behavior and process variations.
- SPICE Simulation Flow: Provides a systematic approach from writing netlists → running simulations → analyzing results.

### <ins>SPICE setup
### 1. Netlist for NMOS
A simple NMOS device shown in Figure 2 was simulated using SPICE.

![WhatsApp Image 2025-08-25 at 23 46 47_2c04e9d6](https://github.com/user-attachments/assets/f3d42c49-f531-4a6f-9e9c-3fe2f644d8f1)

Figure 2: Structure of a simple NMOS device.

```
*Model Description
.param temp=27

*Including sky130 library files
.lib "sky130_fd_pr/models/sky130.lib.spice" tt

*Netlist Description
XM1 Vdd n1 0 0 sky130_fd_pr__nfet_01v8 w=5 l=2
R1 n1 in 55
Vdd vdd 0 1.8V
Vin in 0 1.8V

*Simulation commands
.op
.dc Vdd 0 1.8 0.1 Vin 0 1.8 0.2

.control
run
display
setplot dc1
.endc

.end
```

Notes:
- XM1: Defines the NMOS transistor with width 𝑊=5, length 𝐿=2.
- R1: Added to avoid directly feeding input current into the gate.
- Vdd and Vin: Define supply and input voltages.

### 2. SPICE Simulation Flow
- Write netlist → describe circuit elements.
- Include model libraries → here, SkyWater sky130_fd_pr.
- Set process corner → e.g., tt, ff, ss, sf, fs.

  - Example: <pre> ```spice .lib "sky130_fd_pr/models/sky130.lib.spice" tt ``` </pre>
  - Changing tt → ff or ss changes the process variation.

- Run commands (.op, .dc, .tran, etc.) to simulate.
- Observe waveforms & results in ngspice GUI or terminal.

### Lab Activity – Day 1
- The tt (typical corner) was used.
- Process corner variation (tt → ff → ss) changes drive current & Vt.
- The .dc analysis swept Vdd and Vin to observe NMOS current behavior.
- Output observation: By clicking on the curve in the SPICE GUI, the drain current (𝐼𝐷) can be read directly from y0 in the terminal output.
- Nodes in SPICE are defined by connection points in the netlist.
- Different process corners influence device behavior significantly.
- Practical transistor characteristics can be observed directly from simulation curves.

<img width="1920" height="1030" alt="image" src="https://github.com/user-attachments/assets/53867093-2ac4-4701-9fc7-4d7aef87020f" />

Figure 3: Snapshot of output window of the Day 1 lab activity 

To check the value of 𝐼𝑑 at any point on the curve, left-click on the desired point. The terminal window will display values of 𝑥0 and 𝑦0, where 𝑦0 represents the drain current 𝐼𝑑 in amperes.

# Day 2: Velocity Saturation and basics of CMOS inverter VTC
On the second day of the workshop, we explored advanced concepts of MOSFET device physics and their impact on circuit behavior. Through SPICE simulations, we observed the characteristics of long-channel and short-channel devices, focusing on the effect of velocity saturation at different electric fields. In addition, the operation of MOSFETs as switches and the fundamentals of CMOS inverters were introduced, including their voltage transfer characteristics (VTC).

# Part 1: SPICE simulation for lower nodes and velocity saturation effect
### <ins>Key Learnings:
- Distribution of different regions of operation of NMOS on the Ids–Vds graph.
- The cut-off region occurs when 𝑉𝐺𝑆<𝑉𝑇, where the NMOS remains OFF and no channel is formed.

### Velocity saturation effect:
  - At lower electric fields, carrier velocity is proportional to the field.
  - Beyond a critical electric field (εc), velocity saturates.
  - This alters the current equations at short-channel lengths.

### Regions of operation:
  - Long channel (>250nm): Cut-off, Resistive, Saturation.
  - Short channel (<250nm): Cut-off, Resistive, Velocity Saturation, Saturation.
 
### Lab Activity
In order to analyze the 𝐼𝐷𝑆–𝑉𝐷𝑆 behavior of short-channel devices, the SPICE code shown below is used.
```
*Model Description
.param temp=27

*Including sky130 library files
.lib "sky130_fd_pr/models/sky130.lib.spice" tt

*Netlist Description

XM1 Vdd n1 0 0 sky130_fd_pr__nfet_01v8 w=0.39 l=0.15
R1 n1 in 55

Vdd vdd 0 1.8V
Vin in 0 1.8V

*simulation commands

.op
.dc Vdd 0 1.8 0.1 Vin 0 1.8 0.2

.control

run
display
setplot dc1
.endc

.end
```

<img width="1920" height="1031" alt="image" src="https://github.com/user-attachments/assets/54f61217-eb9a-4972-9413-5a02f4759eee" />

Figure 4: Snapshot of plot window for Ids Vs Vds of short channel device

<img width="799" height="491" alt="image" src="https://github.com/user-attachments/assets/56cf74e1-f9e7-4e26-a1b0-94c81e165e35" />

Figure 5: Velocity saturation effect graph

To calculate the threshold voltage from *IDS VS VGS* curve, the SPICE code shown below is used.
```
*Model Description
.param temp=27

*Including sky130 library files
.lib "sky130_fd_pr/models/sky130.lib.spice" tt

*Netlist Description
XM1 Vdd n1 0 0 sky130_fd_pr__nfet_01v8 w=0.39 l=0.15
R1 n1 in 55

Vdd vdd 0 1.8V
Vin in 0 1.8V

*simulation commands

.op
.dc Vin 0 1.8 0.1

.control

run
display
setplot dc1
.endc

.end
```

<img width="1920" height="1028" alt="image" src="https://github.com/user-attachments/assets/3c259e3d-17f3-4e49-aa3f-96041f35e544" />

Figure 6: Snapshot of plot window showing Ids vs Vgs curve

- Threshold voltage was extracted from the Ids–Vgs curve by extending the linear portion of the graph and finding the x-intercept.

# Part 2: CMOS voltage transfer characteristics (VTC)
### <ins>Key Learnings:
MOSFET as a switch:

OFF resistance is infinite when ∣𝑉𝐺𝑆∣<∣𝑉𝑇∣
ON resistance is finite when ∣𝑉𝐺𝑆∣>∣𝑉𝑇∣

![WhatsApp Image 2025-09-02 at 17 27 23_f630099e](https://github.com/user-attachments/assets/160738ca-d90b-44c4-81a1-45266e91bb7f)

Figure 7: CMOS inverter circuit diagram

Where,
- G = Gate
- S = Source
- D = Drain

### By observation:
- For the NMOS voltage equations

  <img width="156" height="95" alt="image" src="https://github.com/user-attachments/assets/89c8d4ee-1ae4-4da6-b48e-50b3e291aa72" />

- For the PMOS voltage equations

  <img width="213" height="91" alt="image" src="https://github.com/user-attachments/assets/0b1dd3e7-ca7a-4cea-83be-894ebd41028a" />

- For the relationship between the currents IdsN and IdsP

  <img width="148" height="40" alt="image" src="https://github.com/user-attachments/assets/ea32d0dd-c8b3-4388-8a07-d8c013001f79" />

Operation of CMOS inverter:

When 𝑉𝐼𝑁=𝑉𝐷𝐷:

PMOS OFF, NMOS ON → 𝑉𝑂𝑈𝑇=0𝑉


When 𝑉𝐼𝑁=0𝑉
- PMOS ON, NMOS OFF → 𝑉𝑂𝑈𝑇=𝑉𝐷𝐷
	​
![WhatsApp Image 2025-09-02 at 17 27 23_21bd4826](https://github.com/user-attachments/assets/61eedcd7-3410-4596-9d27-9c7cd05b9b71)

Figures 8: Load curve of NMOS transistor

![WhatsApp Image 2025-09-02 at 17 27 23_8c0cc56f](https://github.com/user-attachments/assets/e2891329-8d0b-42a2-9943-3cd3f2bd883b)

Figures 9: Plot IdsP vs VdsP of PMOS transistor

![WhatsApp Image 2025-09-02 at 17 27 24_0a178789](https://github.com/user-attachments/assets/6ca7cc5e-8c14-46a3-afd2-9fd9ae2b683c)

Figure 10: Plot IdsN vs VdsP of PMOS transistor obtained by equating IdsP = -IdsN

![WhatsApp Image 2025-09-02 at 17 27 24_a14d7abb](https://github.com/user-attachments/assets/4db253e4-b8d8-4b37-9617-c51e4d8d3e91)

Figures 11: Load curve of PMOS transistor obtained by the voltage equation Vout = Vdd + VdsP

Load curves of PMOS and NMOS were superimposed to generate the CMOS inverter transfer characteristics.

![WhatsApp Image 2025-09-02 at 17 27 24_7478538a](https://github.com/user-attachments/assets/5bee62f1-6021-4b21-9e9e-dd41272bed87)

Figure 12: Superimposed load curves 
This plot shows *IdsN* vs 𝑉𝑜𝑢𝑡 for different input voltages (𝑉𝑖𝑛)

### Observations from the above graph:
1. ### Intersection Points:
   - The curves of NMOS and PMOS intersect at certain points.
   - These intersection points represent the operating points of the CMOS inverter for different values of input voltage.
2. ### At 𝑉𝑖𝑛=0:
   - PMOS is ON and NMOS is OFF.
   - Output voltage (𝑉𝑜𝑢𝑡) is pulled high (≈𝑉𝐷𝐷).
   - 𝐼𝐷𝑛=0.
4. ### At 𝑉𝑖𝑛=𝑉𝐷𝐷:
   - NMOS is ON and PMOS is OFF.
   - Output voltage (𝑉𝑜𝑢𝑡) is pulled low (≈0).
   - 𝐼𝐷𝑝=0.
5. ### At Intermediate 𝑉𝑖𝑛 (e.g., 0.5 V, 1 V, 1.5 V):
   - Both NMOS and PMOS are ON simultaneously.
   - The drain currents of NMOS and PMOS are equal in magnitude but opposite in direction (𝐼𝐷𝑛+𝐼𝐷𝑝=0).
   - This region corresponds to the transition region of the CMOS inverter.
6. ### Switching Threshold (𝑉𝑚):
   - At around 𝑉𝑖𝑛≈1 V (depending on device sizing), the output voltage rapidly switches.
   - This is the point where the inverter has maximum gain and both transistors conduct.
7. ### Shape of Curves:
   - For lower 𝑉𝑖𝑛, PMOS dominates and pulls the output high.
   - For higher 𝑉𝑖𝑛, NMOS dominates and pulls the output low.
   - The smooth transition between high and low output is visible where curves overlap

![WhatsApp Image 2025-09-02 at 17 27 25_68a8a7d9](https://github.com/user-attachments/assets/a9dbd32d-1385-44d5-82b2-1aa1e9a5b77d)

Figure 13: Plot of 𝑉𝑂𝑈𝑇 vs 𝑉𝐼𝑁

### Observations:
- The CMOS inverter provides a sharp transition from high output to low output as input crosses the switching threshold.
- In the transition region, both NMOS and PMOS conduct simultaneously, ensuring symmetrical switching behavior.
- This characteristic confirms the noise margin and robust logic levels of CMOS inverters.

# Day 3: CMOS switching threshold and dynamic simulations
On the third day of the workshop, the focus was on the Voltage Transfer Characteristics (VTC) of the CMOS inverter and how it defines the inverter’s switching behavior. The concept of switching threshold voltage (Vm) was studied, along with how the PMOS and NMOS transistors operate in different regions depending on the applied input voltage. We also learned how the shape of the VTC is influenced by transistor sizing ratios (Wp/Lp vs Wn/Ln), which in turn affects noise margins and the robustness of the inverter design.

# Part 1: Voltage transfer characteristics and SPICE simulations
### <ins>Key Learnings:
What was learnt:
- A CMOS inverter consists of one NMOS and one PMOS connected in series.
- At any given input voltage (Vin), the operating regions of NMOS and PMOS can be identified (cut-off, linear, or saturation).

![WhatsApp Image 2025-09-02 at 09 59 44_ab56f880](https://github.com/user-attachments/assets/283a410f-69ff-48b1-ab4d-00b1006d70b4)

Figure 14 : The snapshot SPICE netlist considered

The SPICE DECK for the above figure
```
***MODEL Description***
***NETLIST Description***
M1 out in vdd vdd pmos W=0.375u L=0.25u
M2 out in  0   0  nmos W=0.375u L=0.25u

cload out 0 10f

Vdd vdd 0 2.5
Vin  in 0 2.5

***SIMULATION Commands***
.op
.dc Vin 0 2.5 0.05

***.include tsmc_025um_model.mod***
.LIB "tsmc_025um_model.mod" CMOS_MODELS
.end
```

The Voltage Transfer Characteristic (VTC) curve is obtained by plotting Vout vs Vin.The following code is used to obtain the same:
```
*Model Description
.param temp=27

*Including sky130 library files
.lib "sky130_fd_pr/models/sky130.lib.spice" tt

*Netlist Description

XM1 out in vdd vdd sky130_fd_pr__pfet_01v8 w=0.84 l=0.15
XM2 out in 0 0 sky130_fd_pr__nfet_01v8 w=0.36 l=0.15

Cload out 0 50fF

Vdd vdd 0 1.8V
Vin in 0 1.8V

*simulation commands

.op

.dc Vin 0 1.8 0.01

.control
run
setplot dc1
display
.endc

.end
```


Figure 15: Snapshot of VTC curve of CMOS inverter

Key regions of the VTC:
- Vin = 0V: NMOS is OFF, PMOS is ON → Vout ≈ Vdd.
- Vin = Vdd: NMOS is ON, PMOS is OFF → Vout ≈ 0V.
- Vin ≈ Vm (threshold point): Both NMOS and PMOS conduct → inverter switches.

Switching Threshold (Vm):
- Defined as the point where NMOS current = PMOS current.
- A balanced inverter typically has Vm ≈ Vdd/2.
- Vm depends on the sizing ratio (Wp/Lp vs Wn/Ln).

To perform the transient analysis, the following code is needed:
```
*Model Description
.param temp=27

*Including sky130 library files
.lib "sky130_fd_pr/models/sky130.lib.spice" tt

*Netlist Description

XM1 out in vdd vdd sky130_fd_pr__pfet_01v8 w=0.84 l=0.15
XM2 out in 0 0 sky130_fd_pr__nfet_01v8 w=0.36 l=0.15

Cload out 0 50fF

Vdd vdd 0 1.8V
Vin in 0 PULSE(0V 1.8V 0 0.1ns 0.1ns 2ns 4ns)

*simulation commands

.tran 1n 10n

.control
run
.endc

.end
```

# Part 2: Static Behavior Evaluation - CMOS Inverter Robustness: Switching threshold
### <ins>Key Learnings:
- CMOS inverter is a robust device because the shape of it's input versus output curve remains the same for all different values of (W/L) ratios.
- Static Behavior Evaluation: CMOS Inverter Robustness
  - Switching Threshold
  - Noise Margin
  - Power Supply Variation
  - Device Variation
- Switching Threshold Voltage (𝑉𝑚) of CMOS Inverter:
  - The switching threshold voltage 𝑉𝑚 is the point where the input voltage equals the output voltage (𝑉𝑖𝑛=𝑉𝑜𝑢𝑡).
  - Graphical Method:
    To determine 𝑉𝑚, a 45° line (𝑉𝑖𝑛=𝑉𝑜𝑢𝑡) is drawn across the voltage transfer characteristic (VTC) curve of the CMOS inverter. The x-coordinate of the intersection between this line and the inverter’s transfer curve gives the switching threshold.

	For example:

- When 𝑊𝑝/𝐿𝑝=1.5, 𝑉𝑚≈0.98V.
- When 𝑊𝑝/𝐿𝑝=3.75, 𝑉𝑚≈1.2 V

Here, 𝑊𝑝 and 𝐿𝑝 denote the width and length of the PMOS transistor channel.

- Device Operation at 𝑉𝑚:
  - At 𝑉𝑚, both the NMOS and PMOS devices are in conduction because their gate-to-source voltages (𝑉𝐺𝑆) are close to their respective threshold voltages. Thus: Vgs = Vds.
  - The drain currents satisfy the condition: IdsP + IdsN = 0 which implies IdsP = - IdsN.

- Drain Current Equations (ignoring channel-length modulation):

  <img width="394" height="133" alt="image" src="https://github.com/user-attachments/assets/8ba633c6-8b67-4e9d-9939-9db48c45a98e" />

Since IdsP + IdsN = 0, the equation becomes:

<img width="632" height="67" alt="image" src="https://github.com/user-attachments/assets/d4b8fa86-c5f3-407f-bdd8-edeb978de109" />

Solving the above equation for Vm,

<img width="342" height="147" alt="image" src="https://github.com/user-attachments/assets/bba41215-613d-4f80-bc37-ef2e584d23d9" />

Therefore,

<img width="627" height="405" alt="image" src="https://github.com/user-attachments/assets/79974dd0-9aa4-4a1a-891c-735eccf85b13" />

where,

- Wp is the width of the channel in PMOS
- Lp is the length of the channel in PMOS
- Wn is the width of the channel in NMOS
- Ln is the length of the channel in NMOS
- kn' is the process transconductance of the NMOS
- kp' is the process transconductance of the PMOS
- Vdsatn is the Vdsat of the NMOS
- Vdsatp is the Vdsat of the PMOS
- Vm is the switching threshold voltage
- Vt is the threshold voltage
- Vdd is the supply voltage

Adjusting the PMOS dimensions with respect to the NMOS dimensions led us to the following observations.

![WhatsApp Image 2025-09-02 at 09 36 37_11545aec](https://github.com/user-attachments/assets/64aad4c2-9ec4-4dab-8581-531d880c22b2)

Simulation Observations:

- The VTC curve showed three distinct regions:
  - High Output Region (Vin low, Vout ≈ Vdd).
  - Transition Region (Vin ≈ Vm, both transistors conducting).
  - Low Output Region (Vin high, Vout ≈ 0V).

- The sharp transition around Vm indicates strong inverter behavior.
- By changing the ratio (Wp/Lp) / (Wn/Ln), the Vm shifted, showing how sizing affects symmetry and switching speed.

- Figures

  - Figure 18: CMOS Inverter Circuit.
  - Figure 19: VTC Curve (Vout vs Vin).
  - Figure 20: Effect of sizing ratio on VTC.

# Day 4: CMOS Noise Margin Robustness Evaluation 
On the fourth day of the workshop, the focus was on understanding the robustness of CMOS inverters in terms of noise margins. We studied the concepts of V_OH, V_IH, V_IL, and V_OL, which define the valid logic levels of digital circuits, and learned how these values determine the reliability of an inverter under noisy conditions. The equations for Noise Margin High (NM_H) and Noise Margin Low (NM_L) were derived in terms of these voltage levels, providing a theoretical basis for analyzing circuit stability. 


# Part 1: Static Behavior Evaluation - CMOS Inverter Robustness: Noise Margin
### <ins>Key Learnings:
VOH (Output High Voltage): Maximum output voltage interpreted as logic HIGH.

VOL (Output Low Voltage): Maximum output voltage interpreted as logic LOW.

VIH (Input High Voltage): Minimum input voltage recognized as logic HIGH.

VIL (Input Low Voltage): Maximum input voltage recognized as logic LOW.

Noise Margins:

Noise Margin High (NMH):𝑁𝑀𝐻=𝑉𝑂𝐻−𝑉𝐼𝐻


Noise Margin Low (NML):𝑁𝑀𝐿=𝑉𝐼𝐿−𝑉𝑂𝐿

Importance:

- Larger noise margins → inverter is more immune to disturbances.

- Balanced CMOS inverters (Wp/Lp ≈ 2–3 × Wn/Ln) give nearly equal NMH and NML.

Part 2: Lab Activity – Noise Margin Calculation

SPICE Netlist for Noise Margin Simulation:
```
*Model Description
.param temp=27

*Including sky130 library files
.lib "sky130_fd_pr/models/sky130.lib.spice" tt

*Netlist Description

XM1 out in vdd vdd sky130_fd_pr__pfet_01v8 w=1 l=0.15
XM2 out in 0 0 sky130_fd_pr__nfet_01v8 w=0.36 l=0.15

Cload out 0 50fF

Vdd vdd 0 1.8V
Vin in 0 1.8V

*simulation commands

.op

.dc Vin 0 1.8 0.01

.control
run
setplot dc1
display
.endc

.end
```
Simulation Observations:
- The VTC curve was plotted and the slopes at transition points gave VIL and VIH.
- By extracting values from the plot:
  - VOH ≈ 1.8 V
  - VOL ≈ 0 V
  - VIL ≈ ~0.6 V
  - VIH ≈ ~1.2 V

Noise Margins obtained:
- NMH = VOH – VIH ≈ 0.6 V
- NML = VIL – VOL ≈ 0.6 V

This showed that the inverter was robust with balanced noise margins.

Figures

- Figure 21: CMOS Inverter Circuit for Noise Margin Test.
- Figure 22: VTC Curve with VIL and VIH markings.
- Figure 23: Noise Margin High (NMH) and Noise Margin Low (NML) representation.

# Day 5: CMOS Power supply and device variation robustness evaluation 
On the final day of the workshop, we explored how supply voltage variations and manufacturing processes like etching and oxide thickness influence CMOS device performance. We studied the differences between strong and weak transistors (PMOS and NMOS) and observed how inverter behavior changes when moving from Weak PMOS–Strong NMOS to Strong PMOS–Weak NMOS. These experiments helped us understand the practical challenges of circuit design, such as gain variation, device mismatch, and the trade-offs between speed, power, and stability.

# Part 1: Static Behavior Evaluation - CMOS Inverter Robustness: Power Supply Variation
### <ins>Key Learnings:
The supply voltage (VDD) directly affects the Voltage Transfer Characteristic (VTC) of a CMOS inverter.

Increasing VDD:
- Makes the transition slope steeper (higher gain).
- Improves Noise Margins (NMH and NML).
- Leads to faster switching but higher dynamic and static power consumption.

Decreasing VDD:
- Makes the transition slope gentler.
- Reduces Noise Margins.
- Saves power but increases delay and reduces robustness.

Lab Activity:
To analyze the power supply scaling, the followed code is used.
```
*Model Description
.param temp=27

*Including sky130 library files
.lib "sky130_fd_pr/models/sky130.lib.spice" tt

*Netlist Description

XM1 out in vdd vdd sky130_fd_pr__pfet_01v8 w=1 l=0.15
XM2 out in 0 0 sky130_fd_pr__nfet_01v8 w=0.36 l=0.15

Cload out 0 50fF

Vdd vdd 0 1.8V
Vin in 0 1.8V

.control

let powersupply = 1.8
alter Vdd = powersupply
        let voltagesupplyvariation = 0
        dowhile voltagesupplyvariation < 6
        dc Vin 0 1.8 0.01
        let powersupply = powersupply - 0.2
        alter Vdd = powersupply
        let voltagesupplyvariation = voltagesupplyvariation + 1
      end

plot dc1.out vs in dc2.out vs in dc3.out vs in dc4.out vs in dc5.out vs in dc6.out vs in xlabel "input voltage(V)" ylabel "output voltage(V)" title "Inveter dc characteristics as a function of supply voltage"

.endc

.end
```
- A CMOS inverter was simulated with VDD varied from 1.0 V to 2.0 V in steps.
- For each value of VDD, the inverter VTC was plotted.
- VOH, VOL, VIH, and VIL were extracted and Noise Margins calculated.

Observations:
- At VDD = 2.0 V, the inverter showed strong robustness with large noise margins and a sharp transition.
- At VDD = 1.0 V, the inverter’s transition was smoother, noise margins shrank, and the circuit became more sensitive to noise.
- Thus, a trade-off exists between power efficiency and robustness.

# Part 2: Static Behavior Evaluation - CMOS Inverter Robustness: Device Variation
### <ins>Key Learnings:
- In real fabrication, device parameters are never perfectly ideal.
- Variations arise due to:
  - Oxide thickness (tox): Affects threshold voltage (Vth).
  - Etching process errors: Change transistor width/length (W/L).
  - Doping variations: Alter mobility and drive current.

- Strong vs Weak Devices:
  - Strong NMOS / Weak PMOSSwitching threshold (Vm) shifts downward (closer to GND).
  - Output falls faster than it rises.
  - Noise margin high (NMH) reduces, but NML improves.
    
- Strong PMOS / Weak NMOS
  - Switching threshold (Vm) shifts upward (closer to VDD).
  - Output rises faster than it falls.
  - Noise margin low (NML) reduces, but NMH improves.
  
- Balanced Case (Wp/Lp ≈ 2.5 × Wn/Ln)
  - Switching threshold Vm ≈ VDD/2.
  - Both rise and fall times are symmetric.
  - Provides maximum robustness against noise.

Lab Activity:
The following code is used to perform the lab simulation for the device variations:
```
*Model Description
.param temp=27

*Including sky130 library files
.lib "sky130_fd_pr/models/sky130.lib.spice" tt

*Netlist Description

XM1 out in vdd vdd sky130_fd_pr__pfet_01v8 w=7 l=0.15
XM2 out in 0 0 sky130_fd_pr__nfet_01v8 w=0.42 l=0.15

Cload out 0 50fF

Vdd vdd 0 1.8V
Vin in 0 1.8V

*simulation commands

.op

.dc Vin 0 1.8 0.01

.control
run
setplot dc1
display
.endc

.end
```
- CMOS inverters were simulated with three different device strength configurations:
  - Strong NMOS / Weak PMOS
  - Strong PMOS / Weak NMOS
  - Balanced PMOS and NMOS
- VTC curves were compared to analyze the effect of strength imbalance.

Observations:

- When NMOS was stronger, the inverter output pulled down quickly, but high-level noise immunity reduced.
- When PMOS was stronger, the inverter pulled up quickly, but low-level noise immunity reduced.
- Balanced sizing provided the best trade-off with a stable Vm ≈ VDD/2 and symmetric noise margins.

Figures
- Figure 24: VTC curves for CMOS inverter at different VDD values.
- Figure 25: VTC of inverter with Strong NMOS / Weak PMOS.
- Figure 26: VTC of inverter with Strong PMOS / Weak NMOS.
- Figure 27: Comparative plot showing the effect of strength imbalance.

# Conclusion
During the course of this workshop, I was able to gain a deeper understanding of MOSFET operation and CMOS inverter design. I explored how the characteristics of an inverter can be modified through device sizing, power supply variation, and transistor strength adjustments. I also learned to create and analyze SPICE decks from netlists, and perform simulations that closely reflect real-world circuit behavior.

The study of CMOS voltage transfer characteristics and the factors influencing them gave me practical insights into circuit design trade-offs. Additionally, learning about static behavior evaluation — including noise margins, power supply variations, and device robustness — helped me appreciate the importance of reliability in VLSI design.

The hands-on lab activities were especially valuable, as the plots and simulation outputs encouraged me to think critically about parameter variations and their effects. Overall, this workshop has ignited my interest in MOSFETs and CMOS design, motivating me to further master the fundamentals of VLSI and system-level design. My experience with this workshop was truly enriching, and the guidance provided made the entire learning process smooth and impactful.

# Reference
- Skywater Technology Foundry, SKY130 PDK Documentation – https://skywater-pdk.readthedocs.io
- Sedra & Smith, Microelectronic Circuits, Oxford University Press.
- Rabaey, Chandrakasan & Nikolic, Digital Integrated Circuits: A Design Perspective, Pearson Education.
- Ngspice Official Documentation – http://ngspice.sourceforge.net/docs.html
- https://www.vlsisystemdesign.com/
