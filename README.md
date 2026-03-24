# ANTI-GRAVITY-ELEVATOR
# 🚀 Anti-Gravity Elevator DFA Simulator

A **Theory of Computation project** that models an **elevator system using a Deterministic Finite Automaton (DFA)**.  
The simulator demonstrates how formal automata concepts can represent a real-world control system.

The elevator operates in a **zero-gravity environment** and moves between **five floors** based on user commands.

---

# 📌 Problem Statement

Design a **finite automaton for an elevator system** operating in a building with **N floors**.

The automaton should:

- Start at an **initial floor**
- Move **UP or DOWN** between floors
- **STOP** at any floor
- Detect **invalid transitions** such as:
  - Moving up from the top floor
  - Moving down from the ground floor

---

# 🖥 Simulator Features

The interactive simulator includes:

- Elevator shaft visualization
- Floor docking rings
- Animated elevator capsule
- DFA state transition diagram
- Interactive control panel
- Error state alert system

---

# 📊 DFA Properties

### Deterministic
Every state has **exactly one transition per input symbol**.

### Total
All **state–input combinations are defined**.

### Minimal
Using the **Myhill-Nerode theorem**, the DFA is minimal.
