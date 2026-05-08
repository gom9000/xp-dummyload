# PSU Dummy Load eXPerience
A series of documented laboratory experiences on building simple dummy loads to test small PSUs.


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
### **[Resistive Dummy Load for low-power 9V PSU](dummyload-resistor-9)**
**Type**: Passive Resistive | **Complexity**: Low | **Status**: Completed

A "Keep It Simple" approach using a switchable resistive network.

- **Key Features**: Constant Resistance (CR) mode, selectable loads (50mA, 100mA and 200mA on 9V PSU), thermal analysis up to 3.2W.

### **[MOSFET Active Dummy Load for low-power PSU](dummyload-mosfet)**
**Type**: Active Electronic | **Complexity**: Medium | **Status**: Completed

Transitioning from static resistors to linear MOSFET control for adjustable current.

- **Key Features**: CC (Constant Current) mode, adjustable via potentiometer.


## About & License
**Author**: Alessandro Fraschetti (gom9000).<br/>
**License**: This experience is licensed under the [MIT License](LICENSE).<br/>