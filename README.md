# Mains High-Low Voltage Cutoff Circuit 🔌

A hardware circuit designed to automatically disconnect mains power during overvoltage (>270V) or undervoltage (<170V) conditions to protect appliances.

![Circuit Diagram](https://github.com/Mounith-H/Mains-Cutoff-Circuit/blob/main/Circuit%20schematics/Schematic.png)  

---

## Table of Contents
- [Features](#features)
- [Components](#components)
- [Circuit Diagram](#circuit-diagram)
- [How It Works](#how-it-works)
- [Usage](#usage)
- [Safety Notes](#safety-notes)
- [License](#license)
- [Contributing](#contributing)

---

## Features ✨
- **Auto Cutoff**: Disconnects power during voltage fluctuations.
- **4 LED Indicators**: 
  - 1 OverVoltage LED: RED for input has voltage above set threshold, Green for normal.
  - 2 UnderVoltage LED: RED for input has voltage below set threshold, Green for normal.
  - 3 Delay LED: RED for in delay mode.
  - 4 Output LED: RED Output OFF, GREEN Output ON.
- **DELAY ON/OFF**: jumper(J6)) to Enable/Desable dealy.
- **Relay-Based**: Supports high-current loads.

---

## Components 🛠️

| Designators               | Component                      | Footprint                                      | Quantity |  
|---------------------------|--------------------------------|-----------------------------------------------|----------|
| R5, R21, R22, R28, R24, R18 | 10k Resistor                  | Axial DIN0207 (6.3mm x 2.5mm)                | 6        |
| R15, R13, R10, R6, R19, R9, R20, R7, R12, R23, R16 | 1k Resistor          | Axial DIN0207 (6.3mm x 2.5mm)                | 11       |
| U1                        | LM324 Op-Amp IC               | CERDIP-14 (Side-Brazed Socket)               | 1        |
| R17, R11, R14, R8         | 220Ω Resistor                 | Axial DIN0207 (6.3mm x 2.5mm)                | 4        |
| Q4, Q3, Q7, Q2, Q1, Q6    | BC547 Transistor              | TO-92L Wide Package                          | 6        |
| D6, D8, D9, D7            | Dual LED                      | LED D3.0mm-3                                 | 4        |
| D5, D11, D3, D4           | 1N4148 Diode                  | DO-35 Horizontal                             | 4        |
| R4, R25, R2               | 16k Resistor                  | Axial DIN0207 (6.3mm x 2.5mm)                | 3        |
| J4                        | LED Board Header              | 1x06 Pin Header (2.54mm)                     | 1        |
| R1                        | 1.5k Resistor                 | Axial DIN0207 (6.3mm x 2.5mm)                | 1        |
| C2                        | 1µF Capacitor                 | Radial D5.0mm (P2.50mm)                      | 1        |
| RV2, RV1, RV3             | 10k Potentiometer             | Bourns 3296W Vertical Trimmer                | 3        |
| PS1                       | Hi-Link 12V Power Supply      | HLK-5M05 Module                              | 1        |
| D10, D2, D1               | 1N4007 Diode                  | DO-41 Horizontal                             | 3        |
| RV4                       | 5k Potentiometer              | Bourns 3296W Vertical Trimmer                | 1        |
| R26                       | 470k Resistor                 | Axial DIN0207 (6.3mm x 2.5mm)                | 1        |
| C3                        | 100µF Capacitor               | Radial D6.3mm (P2.50mm)                      | 1        |
| F1                        | Fuse                          | Blade ATO (Direct Solder)                    | 1        |
| J2                        | Transformer Terminal Block    | 1x03 Terminal Block (5.00mm)                 | 1        |
| J1, J5                    | AC Input Terminal Block       | Phoenix PT-1.5-2-5.0-H (5.00mm)              | 2        |
| R27                       | 0Ω Jumper Resistor            | Axial DIN0207 (6.3mm x 2.5mm)                | 1        |
| K1                        | Relay (SPDT)                  | SANYOU SRD Series Form-C                     | 1        |
| C1, C4                    | 100nF Capacitor               | 1210 SMD (Hand-Soldered)                     | 2        |
| U2                        | LM78M05 Voltage Regulator     | TO-252-2 Package                             | 1        |


---

## How It Works ⚙️
AC Input → Voltage Sensing → Threshold Comparison → Relay Control → Load Protection  

**Step-by-Step Explanation**

1. AC Input & Isolation
- Mains power (e.g., 220V AC) enters through terminal blocks J1/J5.
- A transformer (connected via J2) steps down the voltage to 12V AC for safe sensing.
- The Hi-Link 12V module (PS1) converts this to 12V DC, while the LM78M05 (U2) regulates it to 5V DC for the control circuitry.

2. Voltage Sensing
- The AC voltage is scaled down using a resistor network (R1, R2, R4, R25, RV1, RV2).
- Potentiometers RV1 and RV2 set the overvoltage (e.g., >270V) and undervoltage (e.g., <170V) thresholds.

3. Threshold Comparison
- The LM324 op-amp (U1) acts as a comparator:
    - One section compares the sensed voltage to the high threshold (set by RV1).
    - Another section compares it to the low threshold (set by RV2).
- If the voltage exceeds either threshold, the LM324 triggers a fault signal.

4. Relay Control
- Fault signals drive BC547 transistors (Q1-Q6) to deactivate the SPDT relay (K1).
- The relay disconnects the load from mains power to prevent damage.

5. Status Indication
- Dual LEDs (D6-D9) indicate system status:
    - Green: Normal operation (voltage within range).
    - Red: Error detected.

- The 470k resistor (R26) and 100µF capacitor (C3) introduce a delay to avoid false triggering.

---

## Usage 🚀  
1. **Power Up**:  
   - Connect mains power to `J1` and load to relay output `J5`.  
2. **Normal Operation**:  
   - **Green LED**: Voltage within safe range (170V–270V).  
3. **Fault Detection**:  
   - **Red LED**: Overvoltage/Undervoltage detected (>270V) or (<170V).  
   - Relay disconnects load automatically.  
4. **Reset**:  
   - **Auto-reset**: Wait for delay (adjustable via `RV4`).  
   - **Manual reset**: Remove short on `J6` pins to restore power immediately.  

---

## Safety Notes ⚠️  
- **High Voltage Risk!** This circuit interacts with mains power.  
  - Use insulated tools and enclosures.  
  - Test with a low-voltage (12V AC) source before connecting to mains.  
- **Fuse Protection**: Ensure `F1` matches your load’s current rating.  
- **No Live Adjustments**: Always power off before adjusting `RV1/RV2/RV3`.  
- **Secure Connections**: Double-check terminal blocks (`J1/J5`) and transformer wiring.  


### Created by [Mounith H] – 📧 mounith.h@gmail.com

## License 📄  
```text
MIT License

Copyright (c) 2023 [Your Name]

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

