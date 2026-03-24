# ANTI-GRAVITY ELEVATOR DFA SIMULATOR — System Prompt
## For Extending the Elevator DFA Project into Zero-G Environment

---

## PROJECT BRIEF

You are implementing an **Anti-Gravity Elevator DFA Simulator** — a variant of the original 5-floor elevator that operates in a **zero-gravity environment with vertical orientation**. The core DFA theory, minimisation proof, and formal structure remain identical to the original project. The changes are **purely architectural and visual**, adapting the elevator's behaviour and display to a weightless setting.

**Core Mandate:** Maintain 100% formal correctness of the DFA (total, deterministic, minimal) while reimagining the physical and visual model for zero-G operation.

---

## DFA FORMAL DEFINITION (UNCHANGED)

The automaton remains:
```
M = (Q, Σ, δ, q₀, F) where:
Q = { F1, F2, F3, F4, F5, q_err }
Σ = { UP, DOWN, STOP }
q₀ = F1
F = { F1, F2, F3, F4, F5 }
```

All transitions, trap state logic, and minimisation proofs apply **exactly as in the original**.

---

## SEMANTIC CHANGES FOR ZERO-G

### 1. Elevator Car Behaviour — No Gravity, No Inertia
- **Traditional model:** Gravity pulls the car downward; motors lift it up. The car coasts to the next floor and gravitational potential energy is managed.
- **Anti-gravity model:** The car floats neutrally in zero-G. UP/DOWN commands impart a constant low-speed drift in that direction. The car has no natural "resting" state — it must be actively held at a floor via magnetic/clamp mechanisms.
- **Philosophical implication:** All floor states (F1–F5) are equally valid resting positions. The absence of gravity eliminates the "ground floor" asymmetry, making the DFA even more symmetric.

### 2. Trap State q_err — Collision or Structural Failure
- **Traditional model:** Boundary violations (UP from F5, DOWN from F1) represent physical impossibilities.
- **Anti-gravity model:** Boundary violations still trigger q_err, but the narrative shifts: rather than "can't go higher/lower," interpret it as a **structural collision or airlock breach**. Once the vessel breaches the containment boundary, the system enters a catastrophic failure state (q_err) and cannot recover without external intervention.

### 3. Input Alphabet Reinterpretation
- **UP:** Thruster burst upward / increase positive Z-axis momentum
- **DOWN:** Thruster burst downward / increase negative Z-axis momentum
- **STOP:** Deactivate thrusters and lock magnetic clamps at current floor (hold position)

---

## VISUAL DESIGN FOR ZERO-G

### 1. Elevator Shaft — Vertical Tube (Updated Aesthetics)

Replace the traditional gravity-centric shaft with a **symmetric vertical tube** design:

```
    ╔═══════════════════════════╗
    ║  ↑ AIRLOCK BOUNDARY (F5)  ║  
    ║                           ║
    ╠═══════════════════════════╣
    ║  ◌◌◌◌◌◌◌ F5 (Top)        ║
    ║  (empty docking bay)      ║
    ╠═══════════════════════════╣
    ║  
    ║  ┏━━━━━━━━━━┓             ║
    ║  ┃ ▓▓▓▓▓ ┃  F4          ║  
    ║  ┃ ▓   ▓ ┃               ║
    ║  ┃ ▓▓▓▓▓ ┃               ║
    ║  ┗━━━━━━━━━━┛             ║
    ║                           ║
    ╠═══════════════════════════╣
    ║  ◌◌◌◌◌◌◌ F3 (Middle)     ║
    ║  (docking ring)           ║
    ╠═══════════════════════════╣
    ║                           ║
    ║  ◌◌◌◌◌◌◌ F2             ║
    ║  (docking ring)           ║
    ╠═══════════════════════════╣
    ║                           ║
    ║  ◌◌◌◌◌◌◌ F1 (Bottom)    ║
    ║  (entry hatch)            ║
    ║  ↓ AIRLOCK BOUNDARY       ║
    ╚═══════════════════════════╝
```

**Design Elements:**
- **Shaft walls:** Bold vertical lines (║) extending top-to-bottom, suggesting a tube/tunnel.
- **Elevator car:** Rounded box-drawing characters (┏ ┓ ┗ ┛ ━ ┃) to give a futuristic, sleek capsule feel.
- **Docking bays:** Represented as concentric rings (◌◌◌◌◌) — visual metaphor for magnetic clamps / bay alignment.
- **Cabin interior:** Animated particle effect using ▓ characters, suggesting floating air/zero-G particles.
- **Airlock boundaries:** Bold markers at F5 (↑) and F1 (↓) showing the hard limits of safe travel.
- **Current position:** Glowing pulses around the car at the active floor.

### 2. Car Animation for Zero-G Motion

When transitioning between floors, animate the car with:
- **Slow, smooth drift** (no sudden acceleration) — reflects low-thrust propulsion.
- **Subtle rotation/tumble** of the cabin ▓ particles — suggests microgravity tumbling.
- **Thruster exhaust visualisation:** Brief ASCII flame/spark (⚡ ✦) below (DOWN) or above (UP) the car as it moves.

### 3. Error State — Breach/Catastrophic Failure

Replace the simple error banner with a **space-disaster aesthetic**:

```
  ╔════════════════════════════╗
  ║                            ║
  ║  ⚠ HULL BREACH — q_err ⚠  ║
  ║  CONTAINMENT FAILURE       ║
  ║  [○○○○○] DECOMPRESSION    ║
  ║                            ║
  ╚════════════════════════════╝
```

The banner should:
- Blink bright red (**#ff4466**) with increased urgency.
- Display a decompression gauge [○○○○○] that slowly empties.
- Include an air-leak visual (curved dashes ≈) floating away.

### 4. DFA Path Diagram — Orbital/Momentum Metaphor

Rather than simple circles, represent states as **orbital nodes** with connecting arc-trajectories:

```
START
(F1) ═══UP═══▶ (F2) ═══UP═══▶ (F3) ═══DOWN═══▶ (F2)
 ◉            ◉            ◉              ◉
(accepting)  (accepting)  (accepting)   (accepting)

(Entry)      (Low Orbit)  (Mid Orbit)   (Return)
```

States in orbit (F2–F4) feel more dynamic; F1 and F5 are boundary markers.

### 5. Header & Branding — Space Theme

Update the ASCII art header to reflect the zero-G setting:

```
    ░▒▓ ANTI-GRAVITY ELEVATOR DFA SIMULATOR ▓▒░
    ═══════════════════════════════════════════════
    ⚡ ZERO-G CONTAINMENT VESSEL v2.0 ⚡
    ═══════════════════════════════════════════════
```

---

## BEHAVIOURAL CHANGES

### 1. Initialisation — F1 as "Entry Hatch" (Not "Ground")
- The machine still starts at **F1** (q₀ = F1), but narratively, F1 is the **entry hatch** or **lowest docking port**, not "ground floor."
- Optionally, display a message on fresh run: "Docked at entry hatch (F1). Ready for ascent/descent."

### 2. All Floors Are Valid Resting States
- The original design already treats all F1–F5 as accepting states, which is **perfect** for zero-G: no floor is "better" to rest at than another.
- Reinforce this by displaying status text at each floor: "F1 (Entry)", "F2 (Low Orbit)", "F3 (Mid)", "F4 (High Orbit)", "F5 (Apex)".

### 3. STOP Command — Magnetic Lock Engagement
- Visually represent STOP as the ship engaging **magnetic docking clamps**:
  - When STOP is selected, the car briefly flashes (⚡) and settles with a lock symbol (🔒 or ⧭).
  - Self-loop edges in the path diagram should pulse/glow to show "holding position."

### 4. Boundary Violations — Physical Impossibility Narrative
- Clearly communicate that attempting to go beyond F5 or below F1 is **impossible**:
  - UP from F5: "Cannot exit containment vessel. Hull breach imminent → q_err."
  - DOWN from F1: "Cannot descend past entry lock. Structural failure → q_err."

---

## UPDATED COLOUR PALETTE

### Zero-G Theme Extension
| Role | Hex | Used For |
|------|-----|----------|
| Deep space | #0a0015 | Page background (slightly deeper void) |
| Nebula glow | #1a1540 | Radial gradient — suggests cosmic light |
| Thruster glow | #00ff88 | Accent colour for UP/DOWN thrust commands (cyan/green) |
| Magnetic lock | #ffaa00 | STOP button, lock symbols (warm, metallic) |
| Hull metal | #aaaaaa | Structural elements, shaft walls (neutral grey) |
| Error (breach) | #ff2255 | q_err state (urgent red, brighter than before) |
| Particle effect | #ccccff | Floating ▓ characters in cabin (icy blue) |
| Scanline | rgba(0,0,0,0.08) | CRT overlay (unchanged, subtle) |

---

## COMPONENT ARCHITECTURE (UNCHANGED)

The React structure remains single-file in `src/App.jsx`:

1. **App** — State management, layout orchestration.
2. **ZeroGElevatorShaft** — Updated shaft rendering with orbital/capsule aesthetics.
3. **DFAPath** — Updated with arc-trajectory connectors instead of straight arrows.
4. **PRDSection** — Now titled "Zero-G Containment System Specifications" with updated narratives.
5. **BreachAlert** — New component replacing simple error banner; displays decompression gauge.

---

## FORMAL REQUIREMENTS CHECKLIST

- [ ] DFA is **total** (all 36 state–input pairs defined, including q_err self-loops).
- [ ] DFA is **deterministic** (exactly one next state per transition).
- [ ] DFA is **minimal** (Myhill-Nerode proof: all 15 state pairs distinguishable).
- [ ] Transition table is **unchanged** from original project.
- [ ] All floor states remain **accepting** (F1–F5 ∈ F).
- [ ] Trap state **q_err is non-accepting and absorbing** (all self-loops).
- [ ] Input alphabet Σ = {UP, DOWN, STOP} — no deviations.
- [ ] Start state q₀ = F1 — unchanged.

---

## IMPLEMENTATION PRIORITIES

### Phase 1: Core Mechanics (Non-Negotiable)
1. Copy the exact DFA transition table from the original.
2. Preserve all state management logic (sequence, path, verdict).
3. Render the zero-G shaft as a vertical tube with capsule-style car.
4. Test that accepted/rejected sequences match original project.

### Phase 2: Visual Polish
1. Implement smooth, drift-like animations for UP/DOWN transitions.
2. Add thruster exhaust visuals (⚡ particles).
3. Redesign DFA path diagram with orbital aesthetics.
4. Implement breach alert with decompression gauge animation.

### Phase 3: Narrative Enhancements
1. Update PRD section with zero-G language.
2. Add floor labels: (Entry), (Low Orbit), (Mid), (High Orbit), (Apex).
3. Display docking/lock messages for STOP actions.
4. Update viva notes to explain zero-G adaptation.

### Phase 4: Stretch Goals
1. Add particle effects (floating debris, thruster flames).
2. Implement pitch/yaw rotation of cabin during transit.
3. Add audio feedback (thruster hum, magnetic lock click).
4. Create a "manual override" mode for testing edge cases.

---

## KEY PRINCIPLES

1. **DFA purity first:** No changes to the formal automaton. All changes are **cosmetic and narrative**.
2. **Zero-G physics intuition:** Every visual choice should reinforce weightlessness, isolation, and containment.
3. **Accessibility:** Maintain readability of state paths and transitions despite new aesthetics.
4. **Minimalist tech stack:** Keep using React + inline CSS; no external libraries. Vite + React 18 as per original.
5. **Educational value:** The simulator should teach DFA theory while immersing the user in a space-station narrative.

---

## TESTING REQUIREMENTS

### Same Test Cases as Original
All sequences that were accepted/rejected in the original must **behave identically** in the zero-G variant:

**Accepted Sequences:**
- UP UP UP UP → F1→F2→F3→F4→F5 ✓
- UP UP STOP → F1→F2→F3→F3 ✓
- UP DOWN → F1→F2→F1 ✓
- STOP STOP STOP → F1→F1→F1→F1 ✓
- UP UP STOP DOWN UP → F1→F2→F3→F3→F2→F3 ✓

**Rejected Sequences:**
- DOWN → F1→q_err ✗
- UP UP UP UP UP → F1→F2→F3→F4→F5→q_err ✗
- UP UP UP UP DOWN DOWN DOWN DOWN DOWN → ...→F1→q_err ✗

---

## VIVA PREPARATION — ZERO-G ANGLE

**Q: How does zero-gravity change the DFA design?**
A: It doesn't—the DFA is unchanged. What changes is the **physical interpretation** of the states and transitions. In zero-G, there's no "natural" resting floor, so the symmetry of the DFA becomes even more apparent. All floors are equally valid accepting states.

**Q: Why is the trap state q_err a "breach" in zero-G?**
A: In a gravity-based system, boundary violations are physical impossibilities (you can't go lower than the ground). In zero-G, you hit the structural boundary of the containment vessel. Crossing it means catastrophic decompression—a narrative that fits the formal notion of an absorbing error state.

**Q: Could you model alternative environments (underwater, moon-base, etc.)?**
A: Yes! The DFA core is environment-agnostic. Any physical system with N discrete stations and directional commands (forward/back, up/down, stop) maps to this structure. The minimisation proof and trap-state logic remain universal.

**Q: Is the zero-G version more or less minimal than the original?**
A: **Equally minimal.** The Myhill-Nerode proof applies identically. All 15 state pairs remain pairwise distinguishable. The 6-state DFA is minimal regardless of whether we interpret floors as vertical gravity-based or orbital zero-G positions.

---

## DELIVERABLES

1. **src/App.jsx** — Single-file React component with all zero-G features.
2. **Updated PRD** — Inline documentation explaining the zero-G variant (include in a collapsible section).
3. **Test report** — Confirm all original test cases pass with identical verdicts.
4. **Viva notes** — Brief Q&A addressing the zero-G design rationale.

---

## TECHNICAL STACK (UNCHANGED)

- **Runtime:** Node.js ≥18, npm ≥9
- **Build:** Vite 5.x
- **UI:** React 18.x + React-DOM
- **Styling:** Inline CSS-in-JS (no external libraries)
- **Animations:** CSS keyframes injected via `<style>` tag
- **Hooks used:** useState, useEffect, useRef (unchanged)

---

## FINAL CHECKLIST

Before submission:

- [ ] DFA transition table verified against original (byte-for-byte identical).
- [ ] All accepted sequences produce ✓ with correct paths.
- [ ] All rejected sequences produce ✗ and enter q_err at correct point.
- [ ] Zero-G visuals are polished, thematic, and don't obscure readability.
- [ ] PRD section updated with zero-G narrative and maintains formal rigour.
- [ ] Code is single-file, self-contained, and runs without external dependencies.
- [ ] Minimisation proof and trap state explanation present and correct.
- [ ] Viva notes prepared addressing the zero-G angle.

---

## CONCLUSION

This project transforms a standard elevator DFA into an immersive zero-gravity simulation while preserving 100% of the underlying formal computer science. The result is a technically rigorous, narratively rich, and visually striking educational tool for learning finite automata theory.

**The DFA remains perfect. Only the story changes.**
