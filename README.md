# PSU Dummy Load eXPerience
A series of documented laboratory experiences on building simple dummy loads to test small PSUs.

These experiences are guided by the **KIS (Keep It Simple)** philosophy, which in our vision includes the "build with what you have" principle. 

Designing with simple or "standard-grade" components requires extra attention to detail to ensure that hardware limitations do not affect the final reliability. Every "added" element, such as a calibration trimmer or a specific resistor network, is strategically chosen to bridge the gap between minimalist resources and more professional-level results.


## Theoretical Background
The type of load leads to classifying these devices as follows:

- **Passive resistive load**: The simplest form, where current depends strictly on the input voltage ($I=V/R$).

- **Active electronic load**: Uses semiconductors (MOSFETs/BJTs) to control the load dynamically.

Within these classifications, we can implement different operational modes:

- **Constant Current (CC)**: The load maintains a fixed current regardless of voltage variations.

- **Constant Voltage (CV)**: The load adjusts current to maintain a fixed voltage across its terminals.

- **Constant Resistance (CR)**: The device emulates a fixed resistor value.

- **Constant Power (CP)**: The load adjusts current as voltage changes to keep $P=V \cdot I$ constant.


## eXPeriences
### **[Resistive Dummy Load for low-power 9V PSU](./dummyload-resistor-9)**
**Type**: Passive Resistive | **Status**: Completed

A simple approach using a switchable resistive network.

- **Key Features**: Constant Resistance (CR) mode, selectable loads (50mA, 100mA and 200mA on 9V PSU), thermal analysis up to 3.2W.

### **[MOSFET Active Dummy Load for low-power PSU](./dummyload-mosfet)**
**Type**: Active Electronic| **Status**: Completed

Transitioning from static resistors to linear MOSFET control for adjustable current.

- **Key Features**: CC (Constant Current) mode, adjustable via potentiometer.


## About & License
**Author**: Alessandro Fraschetti (gom9000).<br/>
**License**: This experience is licensed under the [MIT License](LICENSE). The license applies to all the documentation, schematic files, and PCB layouts provided in this repository.