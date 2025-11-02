# Voltage-Controlled Current Source (VCCS) — Repository

This repository contains the materials for **Design and Implementation of a Voltage Controlled Current Source for PWM Input** (student report by Paavan Sankeerth). The original project report (PDF) is in `docs/`. Summary, usage, specifications, design decisions, and known limitations are documented here.

**Source PDF**: `docs/DESIGN_AND_IMPLEMENTATION_VCCS_PWM_INPUT.pdf`. fileciteturn0file0

---

## Repository structure

```
vccs-repo/
├─ docs/
│  └─ DESIGN_AND_IMPLEMENTATION_VCCS_PWM_INPUT.pdf
├─ src/
│  ├─ netlist_stub.asc
│  └─ simulation-instructions.txt
├─ .gitignore
├─ LICENSE
├─ CONTRIBUTING.md
└─ README.md
```

---

## 1. Usage instructions

### What is included
- Project report PDF with topology, calculations, simulation methodology and results. (See `docs/`.)
- `src/simulation-instructions.txt` — step-by-step instructions to reproduce the LTspice simulation used in the report (manual steps + recommended settings).
- `src/netlist_stub.asc` — a starter LTspice netlist template you can fill in with component values from the report.

### How to use
1. Clone or download this repository.
2. Open `docs/DESIGN_AND_IMPLEMENTATION_VCCS_PWM_INPUT.pdf` to read the design and results. fileciteturn0file0
3. To run simulations:
   - Install LTspice (or LTspice XVII).
   - Open `src/netlist_stub.asc` in LTspice (or create a schematic using the component list in the PDF).
   - Follow `src/simulation-instructions.txt` to run transient analysis and parameter sweeps.
4. For experimental/bench work follow the safety notes in the PDF (use decoupling, TVS diodes, proper power ratings).

---

## 2. Achieved results vs. target

Taken from the simulation results reported in the PDF (simulation): fileciteturn0file0

- **Target**: Output current range 0–5 mA for Vin = 0–5 V.
- **Achieved (simulation)**: Output current 0–5.02 mA (error &lt;1.5%), Load voltage up to 54.8 V, linearity R² ≈ 0.999.
- **Power supplies**: +15 V for op-amp, +55 V load supply (same as target).

Refer to the PDF for plots and measured trace values. fileciteturn0file0

---

## 3. Specifications, design decisions and reasoning

### Target specifications
- Output current: 0–5 mA
- Control voltage (Vin): 0–5 V
- Load voltage range: up to 55 V
- Current accuracy &lt;2%

### Key design decisions (from the report)
- **Topology**: Op-amp driven MOSFET current source (op-amp senses voltage across R4 and drives MOSFET gate to force I_load = Vin/R4). This provides high output impedance and linear control.
- **Sense resistor R4**: 1 kΩ computed from Vin_max/I_load_max = 5 V / 5 mA = 1 kΩ.
- **Op-amp**: LT1013 chosen for low offset and single-supply operation; trade-off: not rail-to-rail output (≈1.5 V saturation).
- **MOSFET**: T2N7002AK (60 V rating, logic-level threshold). Selected to handle VDS and sense current (5 mA).
- **Supply rails**: +15 V op-amp rail to provide adequate gate drive, +55 V load supply to test maximum load voltages.

### Reasoning & tradeoffs
- LT1013 gives good DC accuracy but cannot swing rails — affects low-current precision. Recommendation in report: use rail-to-rail op amp (e.g., LT6003, OPA197) to improve accuracy for currents &lt;0.5 mA.
- The discrete MOSFET solution is simple and inexpensive but introduces temperature dependence and threshold variation. For a production design, a precision current-regulator IC or a buffered sense amplifier is recommended.
- Filtering: input resistor (R1=100 Ω) and C1 (1 µF recommended; increasing to 10 µF reduces transient overshoot) balance stability vs. transient response.

---

## 4. Known limitations

Derived directly from the project report: fileciteturn0file0

- LT1013 output swing limited to ≈1.5 V from supply rails — low-end precision affected for currents below ~0.5 mA.
- MOSFET threshold variation and temperature sensitivity produce small offsets.
- Op-amp sensing at very high VDS (>60 V) requires isolation.
- Minor transient overshoot observed in simulation (recommend increasing C1 and adding gate resistor ~47 Ω and snubber network).

---

## How to publish to GitHub (local steps)

```bash
# inside the repository root
git init
git add .
git commit -m "Initial commit: VCCS project files and documentation"
# create repo on GitHub via web UI or GitHub CLI, then:
git remote add origin git@github.com:<your-username>/vccs-repo.git
git push -u origin main
```

---

## Suggested next steps (if you want me to continue)
- Add the LTspice schematic or raw `.asc` file exported from the author’s simulation (I currently only have the project PDF). fileciteturn0file0
- Add measurement logs, oscilloscope screenshots, BOM, and PCB files if you have a hardware build.
- Replace the netlist stub with a fully working netlist extracted from the original LTspice file.

---

## License

This repository is provided under the MIT License (see `LICENSE`).

---

*Prepared automatically from the uploaded project report.* fileciteturn0file0
