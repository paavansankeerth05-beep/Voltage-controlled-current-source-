## 🧪 Simulation Methodology and Results

### 🖥️ Software
- **Tool Used:** LTspice XVII  
- **Analysis Types:** Transient analysis and parameter sweep  

---

### ⚙️ Simulation Setup
| **Directive** | **Description** |
|----------------|-----------------|
| <code>.tran&nbsp;1s</code> | Runs transient analysis for 1 second |
| <code>.step&nbsp;param&nbsp;R&nbsp;1000&nbsp;10000&nbsp;2000</code> | Varies load resistance from 1 kΩ to 10 kΩ in 2 kΩ steps |
| **Measured Node:** | <code>I(R2)</code> → Load current |

---

### 📊 Results Summary

- For <code>R<sub>4</sub> = 1 kΩ</code>,  
  <code>I<sub>load</sub> = 0 – 5 mA</code> for <code>V<sub>in</sub> = 0 – 5 V</code>.  
- The output current remained **nearly constant** across varying load resistances, confirming high output impedance.  
- The op-amp output (gate drive) swung between **~1 V – 7 V**, providing adequate control for MOSFET operation.  
- A **minor transient overshoot** was observed; can be mitigated by increasing <code>C<sub>1</sub></code> to **10 µF** for improved loop stability.

---

### 🧠 Observations
- The VCCS design demonstrates **excellent linearity** and **current regulation**.  
- Dynamic response can be fine-tuned through compensation capacitor adjustments.  
- Simulation confirms **practical implementability** with the selected LT1013 and T2N7002AK combination.
## ⚠️ Limitations and Trade-offs

### ⚙️ Performance Constraints

- The **LT1013** output swing is limited to  
  <code>V<sub>sat</sub> ≈ 1.5&nbsp;V</code> from the supply rails — reducing precision for very low currents  
  (<code>I<sub>load</sub> &lt; 0.5&nbsp;mA</code>).

- The **T2N7002AK** exhibits **threshold voltage variation**, leading to a minor offset at small  
  <code>V<sub>in</sub></code> levels.

- **Output current** shows slight dependence on **MOSFET temperature**, due to drain current drift with junction heating.

- The **op-amp** cannot directly sense load current at very high  
  <code>V<sub>DS</sub> &gt; 60&nbsp;V</code> without proper **isolation** or additional protection circuitry.

---

### 🧩 Design Trade-offs Summary

| **Aspect** | **Trade-off / Limitation** | **Potential Mitigation** |
|-------------|-----------------------------|---------------------------|
| Low-current accuracy | Limited by <code>V<sub>sat</sub></code> | Use rail-to-rail op-amp |
| MOSFET threshold drift | Causes minor offset | Device selection or calibration |
| Temperature dependence | Drain current drift | Add thermal compensation or heatsink |
| High-voltage sensing | Unsafe for >60 V | Use isolation amplifier or sense transformer |

  
