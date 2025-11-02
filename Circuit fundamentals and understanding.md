## ⚙️ 1. Topology Selection and Justification

The chosen topology is a **Voltage-Controlled Current Source (VCCS)** implemented using:  
- An operational amplifier (**LT1013**)  
- An N-channel MOSFET (**T2N7002AK**)  
- A sense resistor (**R4**)  

The op-amp forces the voltage across **R4** to follow the input control voltage <code>V<sub>in</sub></code>, ensuring that the load current remains **directly proportional** to the input voltage.  
This provides precise current regulation suitable for analog control and testing applications.

---

## 🔍 Principle of Operation

- The operational amplifier compares the input voltage <code>V<sub>in</sub></code> with the feedback voltage  
  <code>V<sub>s</sub> = I<sub>load</sub> × R<sub>4</sub></code>.

- It adjusts the MOSFET gate voltage dynamically so that  
  <code>V<sub>s</sub> = V<sub>in</sub></code>.

- Therefore,  
  <p align="center"><code>I<sub>load</sub> = V<sub>in</sub> / R<sub>4</sub></code></p>

---

### ✅ This configuration provides:
- High **output impedance**  
- **Linear** relationship between control voltage and output current  
- **Easy current scaling** through resistor <code>R<sub>4</sub></code>

---

### 🎛️ Op-Amp Selection

The **LT1013** dual op-amp is selected because of:
- Low input **offset voltage**  
- **Single-supply** operation capability  
- Wide operating voltage range (**0 – 30 V**)  
- Excellent suitability for **precision analog control circuits**

  
## 2. Key Design Calculations
## Design Targets and Component Selection

### 🎯 Target
- **Output current range:** <code>I<sub>load</sub> = 0 – 5&nbsp;mA</code>  
- **Control voltage range:** <code>V<sub>in</sub> = 0 – 5&nbsp;V</code>

---

### 1️⃣ Current-Setting Resistor (R4)

<p align="center">
  <code>I<sub>load</sub> = V<sub>in</sub> / R<sub>4</sub></code><br>
  <code>R<sub>4</sub> = V<sub>in,max</sub> / I<sub>load,max</sub> = 5&nbsp;V / 5&nbsp;mA = 1&nbsp;kΩ</code>
</p>

---

### 2️⃣ MOSFET Selection

| **Parameter** | **Requirement** | **Chosen Device: T2N7002AK** |
|----------------|------------------|-------------------------------|
| <code>V<sub>DS(max)</sub></code> | ≥ 55 V | 60 V |
| <code>I<sub>D</sub></code> | ≥ 5 mA | 115 mA |
| <code>V<sub>GS(th)</sub></code> | ≤ 2 V | Logic-level compatible |
| <code>R<sub>DS(on)</sub></code> | — | ≈ 7 Ω |

---

### 3️⃣ Power Dissipation

<p align="center">
  <code>P<sub>MOSFET</sub> = V<sub>DS</sub> × I<sub>load</sub> ≈ (55 V − V<sub>load</sub>) × 5 mA ≈ 0.27 W</code><br>
  <em>Safe within device limits.</em>
</p>

<p align="center">
  <code>P<sub>R4</sub> = I<sub>load</sub><sup>2</sup> × R<sub>4</sub> = (5 mA)<sup>2</sup> × 1 kΩ = 25 mW</code>
</p>

---

### 4️⃣ Input Conditioning

| **Component** | **Value** | **Function** |
|----------------|------------|---------------|
| **R1** | 100 Ω | Limits input current to op-amp |
| **C1** | 1 µF | Filters high-frequency transients |

## ⚡ Power Supply Requirements and Selection

### 🔋 3️⃣ Power Sources

- **Op-amp Supply (V<sub>3</sub>):** +15 V single-supply chosen to provide sufficient gate drive range for the MOSFET.  
- **Load Supply (V<sub>2</sub>):** 55 V DC source representing the external load power supply.  
- **Control Input (V<sub>1</sub>):**  
  <code>PULSE(0&nbsp;5&nbsp;0&nbsp;1µ&nbsp;1µ&nbsp;2.5m&nbsp;5m&nbsp;100)</code>  
  → Square wave varying between 0 V and 5 V to test linear current response.

---

### 🧩 Decoupling and Stability
- Power rails are **decoupled using 0.1 µF capacitors**, as recommended for physical implementation.  
- Decoupling ensures:
  - Noise suppression from switching transients  
  - Improved op-amp stability  
  - Reduced susceptibility to high-frequency interference  

---

**Summary:**
| Supply | Voltage | Purpose |
|---------|----------|----------|
| <code>V<sub>1</sub></code> | 0–5 V | Control signal (test input) |
| <code>V<sub>2</sub></code> | 55 V DC | Load supply |
| <code>V<sub>3</sub></code> | +15 V | Op-amp power rail |

