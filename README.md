# Piezoelectric Energy Harvesting in Pedestrian Walkways

This repository documents the **hardware implementation and prototype validation**
of a piezoelectric energy harvesting system designed for pedestrian walkways.

The **theoretical background, feasibility study, economic analysis, and formal results**
are provided in the accompanying research paper located in the `paper/` directory.
This repository focuses strictly on **system architecture, circuit implementation,
and experimental behavior**.

---

## Project Scope

- Harvest mechanical energy from pedestrian footsteps using piezoelectric elements
- Demonstrate limitations of raw piezoelectric output
- Implement rectification and energy storage for output stabilization
- Integrate sensor-based lighting control to reduce energy consumption
- Validate system behavior through laboratory-scale prototypes

---

## System Overview

The system converts pedestrian-induced mechanical stress into electrical energy using
piezoelectric elements. The generated energy is conditioned and stored before being
used to support low-power lighting applications.



<p align="center">
  <img src="figures/concept-flow.png" width="500">
</p>


---
## Components Used and Their Roles

This project was implemented using two hardware configurations:
1. A **direct piezoelectric output circuit** (without rectification or storage)
2. A **conditioned energy harvesting circuit** (with rectification and capacitive storage)

The following components were used across the two configurations.

---

### 1. Piezoelectric Sensors (×4)

**Purpose**
- Convert mechanical stress from pedestrian footsteps into electrical energy.

**Configuration**
- Four piezoelectric discs were connected in a **series–parallel configuration**.

**Reason for configuration**
- Series connection increases output voltage.
- Parallel connection increases current capability.
- The combined configuration provides a better balance for energy harvesting than using a single element.

**Usage**
- Used in both prototype circuits (with and without rectification).

---

### 2. Resistors

#### a) 100 kΩ Resistor

**Purpose**
- Voltage stabilization and protection.
- Prevents excessive voltage from damaging Arduino input pins.

**Usage**
- Connected across the piezoelectric output when interfacing with the Arduino.
- Used primarily in the **direct piezo output prototype** to limit current during voltage spikes.

---

#### b) 10 kΩ Resistor

**Purpose**
- Pull-down / voltage reference resistor.

**Usage**
- Used with the piezoelectric sensor input to stabilize analog readings.
- Used with the LDR as part of a voltage divider for ambient light sensing.

---

### 3. Diodes (×4)

**Purpose**
- Construct a **full-wave bridge rectifier**.

**Why needed**
- Piezoelectric sensors generate an alternating (AC) voltage.
- Lighting systems and energy storage require direct current (DC).

**Usage**
- Used only in the **second prototype circuit**.
- Four diodes form a bridge rectifier that converts AC output from the piezo array into DC.

---

### 4. Capacitor

**Purpose**
- Energy storage and voltage smoothing.

**Why needed**
- Piezoelectric output consists of short voltage spikes.
- A capacitor accumulates energy over multiple footsteps and smooths the output voltage.

**Usage**
- Used only in the **rectified circuit**.
- Connected after the bridge rectifier to store harvested energy.
- Enables gradual voltage buildup and more stable output.

---

### 5. Arduino Uno

**Purpose**
- Monitoring, control, and logic implementation.

**Role**
- Reads voltage levels from the piezoelectric system or storage capacitor.
- Implements control logic for lighting activation.
- Interfaces with sensors (LDR) and output devices (LED, LCD).

**Important note**
- The Arduino does **not** power the system.
- It acts only as a control and measurement unit.

---

### 6. LED

**Purpose**
- Visual indication of harvested energy availability.
- Demonstration of lighting activation.

**Usage**
- In the direct piezo prototype, the LED turns on briefly due to voltage spikes.
- In the rectified and stored prototype, the LED operates more consistently.

---

### 7. Light Dependent Resistor (LDR)

**Purpose**
- Ambient light sensing for energy-saving control.

**Why used**
- To prevent unnecessary lighting during daylight conditions.
- To demonstrate demand-side energy efficiency.

**Usage**
- Combined with a 10 kΩ resistor to form a voltage divider.
- Arduino reads the LDR value and enables lighting only when ambient light is low.

---

### 8. LCD Screen

**Purpose**
- System feedback and visualization.

**Usage**
- Displays measured voltage levels or system status.
- Helps verify energy accumulation and system behavior during testing.

---

### 9. Breadboard

**Purpose**
- Rapid prototyping and testing.

**Usage**
- Used to assemble and modify circuits without soldering.
- Allowed comparison between the unconditioned and conditioned prototypes.

---

## Circuit Comparison Summary

| Feature | Prototype 1 | Prototype 2 |
|------|-----------|------------|
| Rectifier | No | Yes |
| Capacitor | No | Yes |
| Output Stability | Very low | Significantly improved |
| Energy Storage | None | Present |
| LED Behavior | Short flashes | More sustained operation |

---

The comparison between the two circuits highlights the necessity of **rectification and energy storage** for practical piezoelectric energy harvesting applications.

## Prototype Implementations

### Prototype 1: Direct Piezoelectric Output (Unconditioned)

This prototype connects the piezoelectric array directly to the load without any
energy conditioning stage.

**Observed behavior**
- Output consists of short, high-voltage spikes
- LED turns on briefly and inconsistently
- No sustained or usable energy output

**Conclusion**
Raw piezoelectric output is unstable and unsuitable for direct lighting applications.

---

### Prototype 2: Rectifier and Energy Storage (Conditioned Output)

To stabilize the output, a full-wave bridge rectifier and a storage capacitor were added.


<p align="center">
  <img src="figures/IMG_9136.PNG" width="350">
</p>



**Observed behavior**
- AC output converted to DC
- Energy accumulates over repeated footsteps
- Significantly improved voltage stability
- Suitable for controlled low-power operation

This prototype validates the necessity of rectification and storage in piezoelectric
energy harvesting systems.

---

## Circuit Implementations



### Raw Piezoelectric Circuit
<p align="center">
  <img src="circuits/raw-piezo-circuit.png" width="450">
</p>

### Rectifier and Storage Circuit
<p align="center">
  <img src="circuits/rectifier-storage-circuit.png" width="450">
</p>
---

## Arduino Integration

An Arduino microcontroller is used for:
- Monitoring voltage across the storage capacitor
- Implementing control logic
- Interfacing with lighting components

The Arduino does not supply energy to the system; it acts solely as a monitoring
and control unit.

---

## Sensor-Based Lighting Control (Energy Saving)

To reduce unnecessary energy consumption, the system integrates an
**LDR (Light Dependent Resistor)**.

![LDR lighting control](figures/ldr-lighting-control.png)

**Control logic**
- Lighting activates only when ambient light is insufficient
- Prevents energy usage during daylight conditions
- Demonstrates demand-side energy efficiency

This method complements energy harvesting by reducing overall energy demand.

---

## Documentation

- Full research paper: `paper/Piezoelectric_Energy_Harvesting_Birzeit.pdf`
- Project poster: `figures/poster.png`

![Poster](figures/poster.png)

---

