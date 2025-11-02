# VCCS - Op-Amp + MOSFET Voltage-Controlled Current Source

This repository contains LTspice-ready netlists, a design report, and BOM for a Voltage-Controlled Current Source (VCCS) that converts a 0–5 V control signal (filtered PWM) into a 0–5 mA regulated current through a load.

## Contents
- netlists/ideal_test.net — Ideal-op-amp version for functional validation.
- netlists/realistic_test.net — Realistic netlist (uses high-gain E-source as placeholder; instructions included to replace with LT1013 or other op-amp).
- report/Design_Report.md — 3–5 page design report describing topology, calculations, simulation results, limitations and recommendations.
- bom/BILL_OF_MATERIALS.md — Parts list and suggested equivalents.
- scripts/plot_instructions.md — How to run the netlists in LTspice and what to plot.

## How to run (quick)
1. Install LTspice (Analog Devices).
2. Copy one of the *.net files into a new file and open in LTspice, or open LTspice and paste the netlist.
3. Run transient: .tran command is included.
4. Plot I(RSENSE) or I(RLOAD) to view regulated current.

## License
MIT — see LICENSE.

If you want a ready .asc schematic instead of netlist, ask and I will provide it.
 
