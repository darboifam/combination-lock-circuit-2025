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

## Documentation

- 📄 Full Report: [`report/EGR211FinalProjectReport.pdf`](report/EGR211FinalProjectReport.pdf)
- 🧾 Editable Report Source: [`report/Final_Project.docx`](report/Final_Project.docx)

### Key Figures / Photos
- Multisim schematic:
  - ![Schematic](assets/schematic_multisim.png)
- Breadboard builds:
  - ![Tumbler](assets/breadboard_tumbler.jpg)
  - ![Win Branch](assets/breadboard_win.jpg)
  - ![Lose Branch](assets/breadboard_lose.jpg)
  - ![Arduino + Buzzers](assets/breadboard_arduino_buzzers.jpg)

### Measurements (Tables / Scope)
- Tumbler voltage table: ![Tumbler Table](assets/table_tumbler_outputs.png)
- Comparator thresholds: ![Comparator Table](assets/table_comparator.png)
- 555 timing and I/O: ![555 Tables](assets/table_555_values.png)
- Oscilloscope captures:
  - ![Node Voltage](assets/scope_waveforms/scope_node_voltage.jpg)
  - ![Win/Lose Timers](assets/scope_waveforms/scope_win_lose.jpg)
  - ![Alarm Response](assets/scope_waveforms/scope_alarm.jpg)

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

## Reproducing the Build

1. Build the **tumbler network** on the breadboard and verify the combination node voltage changes.
2. Add the **comparators** and verify the output flips around the chosen threshold.
3. Add **555 timers** for the Win/Lose outputs and verify timed pulses.
4. Add the **Arduino + buzzers** for 3-attempt alarm behavior.
5. Capture measurements (DMM + scope) and compare to the report tables.

---

## Notes / Lessons Learned

- Edge-triggering behavior can occur when pressing and releasing confirm (comparator transitions can trigger timers more than once).
- Breadboard builds can introduce timing variation vs calculations (component tolerance + parasitics).

---

## License

Choose one:
- MIT (simple open-source)  
- or “All rights reserved” if you only want it as class documentation

---

## Acknowledgements

Thanks to the EGR 211 course staff and lab resources used for measurement and validation.
