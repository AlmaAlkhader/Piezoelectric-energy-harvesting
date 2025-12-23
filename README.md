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

![Conceptual flow](figures/concept-flow.png)

---

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

<img src="figures/IMG_9136.PNG" width="350">


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
![Raw piezo circuit](circuits/raw-piezo-circuit.png)

### Rectifier and Storage Circuit
![Rectifier circuit](circuits/rectifier-storage-circuit.png)

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

