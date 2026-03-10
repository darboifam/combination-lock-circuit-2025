# Electronic Combination Lock System (EGR 211 Final Project)

An electronic combination lock built using an **analog resistor/switch “tumbler” network** to generate a single decision voltage, **LM393 comparators** to classify the code as correct/incorrect, **NE555 timers** to generate timed visual outputs, and an **Arduino** to count failed attempts and trigger an alarm on the third incorrect entry.

> Course: EGR 211 (Montgomery County Community College)  
> Date: Dec 15, 2025  
> Team: Gabriel Moody, David Williams, Caleb Karlson, Tyler Jackson

---

## Project Overview

The system uses an analog keypad/tumbler network to produce a **combination node voltage**:
- **Correct combination** pulls the node **low** (unlock condition)
- **Incorrect/partial combinations** leave the node **high** (lock condition)

That node is evaluated by comparator stages that drive:
- **Win branch**: green LED (timed “unlock” indicator)
- **Lose branch**: red LED (locked indicator behavior)
- **Arduino branch**: beeps on the first two incorrect attempts, and triggers a sustained alarm on the third attempt

---

## Demo / Behavior Summary

### Inputs
- 8 keypad switches (code entry)
- 1 confirm switch (submits the entered code)

### Outputs
- Green LED: timed unlock indication (Win branch)
- Red LED: locked indication (Lose branch)
- Buzzers: short beeps for first two wrong attempts, sustained alarm for the third attempt

---

## Circuit Architecture (High Level)

1. **Tumbler Network (Analog Keypad)**
   - Resistor/switch network creates a voltage divider at the combination node.
   - Confirm switch isolates the node until evaluation.

2. **Comparator Stage (LM393)**
   - Thresholds set so the correct combination falls on the “unlock” side of the decision boundary.

3. **Timing Stage (NE555 Monostables)**
   - Timed pulses for Win/Lose indicators.
   - Separate timer path used for alarm duration.

4. **Arduino Monitoring + Alarm Logic**
   - Reads the “code state,” increments a counter on incorrect attempts.
   - 1st & 2nd incorrect: short beep pulse.
   - 3rd incorrect: triggers alarm output for a sustained buzzer event, then resets.

---

## Report

- 📄 Final Report (PDF): [EGR211FinalProjectReport.pdf](report/EGR211FinalProjectReport.pdf)
---

## Photos

### MultiSIM Circuit Diagram
![MultiSIM Circuit Diagram](<assets/photos/MultiSIM Circuit Diagram.png>)

### Tumbler System
![Tumbler System](<assets/photos/Tumbler System.png>)

### Win Branch
![Win Branch](<assets/photos/Win Branch.png>)

### Lose Branch
![Lose Branch](<assets/photos/Lose Branch.png>)

### Arduino System and Buzzers
![Arduino System and Buzzers](<assets/photos/Arduino System and Buzzers.png>)

### IO Table and Case Measurements
![IO Table and Case Measurements](<assets/photos/IO Table and Case Measurements.png>)

### IC555 Measurements and IO Table
![IC555 Measurements and IO Table](<assets/photos/IC555 Measurements and IO Table.png>)

---

## Bill of Materials (Typical)

- LM393 comparator IC(s)
- NE555 timer IC(s)
- Arduino (for attempt counter + alarm trigger)
- Resistors (various values as in schematic)
- Capacitors (timing + decoupling)
- LEDs + current-limiting resistors
- Switches (8 keypad + 1 confirm)
- Buzzers
- Breadboard + jumper wires
- Power supply rails (per your build configuration)

> See the report/schematic for exact values and measured results.

---

## Notes / Lessons Learned

- Edge-triggering behavior can occur when pressing and releasing confirm (comparator transitions can trigger timers more than once).
- Breadboard builds can introduce timing variation vs calculations (component tolerance + parasitics).

---

## Acknowledgements

Huge thank you to Professor Moorthy and Professor Vardakas for all the assistance!
