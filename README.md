# Mains High-Low Voltage Cutoff Circuit 🔌

A hardware circuit designed to automatically disconnect mains power during overvoltage (>270V) or undervoltage (<170V) conditions to protect appliances.

![Circuit Diagram](image.png)  
*(Upload `image.png` to your repo and update the link above)*

---

## Table of Contents
- [Features](#features)
- [Components](#components)
- [Circuit Diagram](#circuit-diagram)
- [How It Works](#how-it-works)
- [Installation](#installation)
- [Usage](#usage)
- [Safety Notes](#safety-notes)
- [License](#license)
- [Contributing](#contributing)

---

## Features ✨
- **Auto Cutoff**: Disconnects power during voltage fluctuations.
- **LED Indicators**: 
  - Red: Overvoltage detected.
  - Green: Normal voltage range.
  - Yellow: Undervoltage detected.
- **Manual Reset**: Push-button to restore power after cutoff.
- **Relay-Based**: Supports high-current loads.

---

## Components 🛠️
Based on your `图例` (legend):
| Label | Component              | Description                     |
|-------|------------------------|---------------------------------|
| A1    | Voltage Sensor Module  | Measures AC mains voltage.      |
| B1    | Comparator IC (LM393)  | Compares voltage to thresholds. |
| C1    | Relay (12V, 10A)       | Switches mains power on/off.    |
| D1    | LED Indicators         | Visual status feedback.         |
| E1    | Transformer (220V-12V) | Steps down voltage for control. |
| F1    | Push Button            | Manual reset after cutoff.      |

*(Update this table to match your actual components!)*

---

## How It Works ⚙️
1. The **voltage sensor** monitors the AC input.
2. The **comparator** checks if voltage exceeds safe thresholds.
3. If unsafe:
   - **Relay** disconnects the load.
   - **LED** indicates fault type.
4. Press the **reset button** to reconnect power once voltage stabilizes.

---

## Installation 🔧
1. **Hardware**:
   - Assemble the circuit as shown in `image.png`.
   - Use a PCB or breadboard for prototyping.
   - Connect to mains via a 220V/12V transformer for isolation.
2. **Software** (if applicable):
   ```bash
   git clone https://github.com/your-username/Mains-Cutoff-Circuit.git