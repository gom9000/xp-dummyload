# MOSFET active dummy load for low-power PSU

## Background and Goal
Design and development of a simple **active MOSFET dummy load** to test low-power Power Supply Units (PSUs) with current rating up to $1A$.

![built](dummyload-mosfet.jpg)


## Requirements
- Control Supply ($V_{cc}$): $9\text{V}$ to $15\text{V}$ DC (Recommended $12\text{V}$).
- Input Voltage: Up to $30\text{V}$ (depending on MOSFET $V_{ds}$ and thermal dissipation).
- Current Range: $0\text{A}$ to $1\text{A}$ (adjustable).
- Operating Mode: Constant Current (CC).
- Power Dissipation: Safe continuous operation up to $\approx 12\text{--}15\text{W}$ with provided heatsink.
- Control: Fully analog, minimalist design (Op-Amp + MOSFET).


## Design

#### Schematic
![board-schematic](hardware/dummyload-mosfet_sch.jpg)

#### Circuit Analysis
The circuit operates as a closed-loop current regulator. The Op-Amp ($U1b$) compares the reference voltage from $P1$ with the feedback voltage across the shunt resistor $R7$.

The MOSFET must dissipate a power of $P = (V_{psu} - V_{R7}) \cdot I$.<br/>
At $1\text{A}$ with $R7 = 1.2\Omega$, the formula is $(V_{psu} - 1.2\text{V}) \cdot 1\text{A}$.

The use of a $2.7\text{V}$ Zener diode ($DZ$) and an Op-Amp buffer ($U1a$) ensures a stable reference, decoupling the control logic from supply voltage fluctuations.

*Note: While $R7$ dissipates a small constant power ($\approx 1.2\text{W}$ @ $1\text{A}$), the MOSFET $Q1$ bears the main thermal stress, which increases linearly with $V_{psu}$.*

The MOSFET used is an **STP3NC60** ($600\text{V}$, $3\text{A}$). Its relatively high $R_{ds(on)}$ $(3.3\Omega)$ defines the minimum operating voltage (**Compliance Voltage**) at high currents ($1A$):

$$V_{compliance} \approx I \cdot (R_{ds(on)} + R_7) = 1\text{A} \cdot (3.3\Omega + 1.2\Omega) = 4.5\text{V}$$

This means the load can maintain $1\text{A}$ only if the PSU supply provides at least $4.5\text{V}$.

**Control Supply($V_{cc}$)**:<br/>
The control logic (Op-Amp) requires a dedicated supply voltage ($V_{cc}$) to drive the MOSFET Gate.
- Recommended $V_{cc}$: $9\text{V}$ to $15\text{V}$ (Standard $12\text{V}$ DC adapter).
- Minimum $V_{cc}$: Approximately $8\text{V}$. This limit is due to the MOSFET's Gate threshold voltage ($V_{gs(th)} \approx 4.5\text{V}$) plus the voltage drop across the shunt resistor ($1.2\text{V}$) and the Op-Amp's internal output swing limitation ($\approx 2\text{V}$ below $V_{cc}$).
- Maximum $V_{cc}$: $30\text{V}$ (Limited by the LM358 and the $2.7\text{V}$ Zener biasing resistor $R1$).

*Note: The STP3NC60 was selected due to immediate availability, although it is not optimized for low-voltage linear operation because of its relatively high Rds(on).*


## Implementation and Test
#### PCB Layout
The circuit was assembled on a custom PCB (protoboard $30 \times 70mm$) designed with ExpressPCB.
![board-pcb](hardware/dummyload-mosfet_pcb.jpg)

#### Calibration Procedure
The circuit offers two ways to calibrate the full-scale current ($1A$ target at maximum $P1$ position).

**Method A: Theoretical (Voltage-based)**<br/>
This method assumes $R7$ is exactly $1.2\Omega$.
With $P1$ set to its maximum position, adjust trimmer $Tr1$ until the voltage at pin 3 of $U1$ reaches $1.2V$. This ensures that at full scale, the load draws exactly $1A$ (given $I = V_{ref} / R7$).

**Method B: Empirical (Current-based)**<br/>
Since the shunt resistor $R7$ has a wide tolerance, to calibrate the device:
1. Connect a reliable Ammeter in series with the PSU under test.
2. Set the user potentiometer $P1$ to its maximum position.
3. Adjust trimmer $Tr1$ until the Ammeter reads exactly $1.00A$.

#### Test Log
The circuit was tested using a **GVDA 30V/10A** switching laboratory power supply. Component temperature was measured using a **GVDA GD128** digital multimeter. Tests were conducted in a closed, non-ventilated environment with an ambient temperature of $21^\circ C$.

**Test 1 (Active Load - CC Mode)**:
- Input Voltage: $9.00V$ (External PSU)
- Control Supply: $12V$ (Fixed)
- Initial State: $1.000A$ @ $21^\circ C (9W)$
- Final State (after 10 min): $0.992A$ @ $71^\circ C$

Observations: The circuit demonstrated good stability with a current drift of only $0.8$%, despite a significant thermal increase of $50^\circ C$.

## Conclusions
**Results**: The project successfully achieves a stable constant current load using a minimal component count. The test log shows that even with a $50^\circ C$ temperature rise, the current drift remains under $1$%, making it a reliable tool for hobbyist PSU testing.
  
**Suggestions**: Adding a small fan to increase the power handling capability.

**Evolutions**: Experimenting with lower $R_{ds(on)}$ MOSFETs to extend the current regulation range at low PSU voltages (below $5V$).


## About & License
**Author**: Alessandro Fraschetti (gom9000).<br/>
**Technical Notes**: The hardware design was supported by **ExpressPCB** and the custom **[expresspcb-goslib](https://github.com/gom9000/expresspcb-goslib)** libraries.<br/>
**License**: This experience is licensed under the [MIT License](LICENSE).<br/>
