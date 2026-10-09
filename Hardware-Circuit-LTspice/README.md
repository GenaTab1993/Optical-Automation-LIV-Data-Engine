# Analog Laser Driver & Power Condition Sub-System (LTspice Simulation Node)

## Module Overview
This sub-folder houses the raw analog schematic source files (`.asc`) validating the electrical security and transient protection stages of the laser diode driver footprint.

## Circuit Parameter Specifications & Test Phases

### 1. AC-DC Filtration & Regulation (`Project_2_Rectifier.asc`)
*   **Topology:** Single-ended half-wave rectifier matted to a parallel Zener shunt regulator.
*   **Filtering Spec:** Enforces a variable decoupling smoothing capacitor benchmarked at **100µF**.
*   **Validation Result:** Suppresses AC power rail ripple voltage by **90%** (dropping from a noisy 5.1V swing down to a stable 0.5V band), successfully stabilizing emitter intensity and preventing sensor artifacting.
*   **Inrush Risk Mitigation:** Transient stress testing isolates an inrush current spike of **640mA** at cold-start turn-on, establishing the parameters for backend current-limiting protection.

### 2. Low-Side MOSFET Switching Driver (`Project_1_MOSFET.asc`)
*   **Topology:** Low-side enhancement-mode N-Channel MOSFET (`2N7002` in SOT-23 package) gated via an MCU logic control pulse (0V Low to 5V High, 50% Duty Cycle).
*   **Suppression Element:** Fast-switching commutation flyback diode (`1N4148`) installed directly in parallel across the inductive load configuration.
*   **Validation Result:** Under unprotected inductive switching (Phase B), the instantaneous collapse of current (di/dt) forces a severe avalanche breakdown spike peaking at **~50V**. Activating the flyback diode (Phase C) instantly clamps the inductive kickback ceiling to a secure, non-destructive plateau of **9.7V** (\(V_1 + V_f = 9.0V + 0.7V\)).

---
*For the complete automated software control execution architecture, refer to the master Python engine in the root directory.*
