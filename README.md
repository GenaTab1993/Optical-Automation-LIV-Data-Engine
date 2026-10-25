# Multi-Instrument Automated Test Executive & Silicon Telemetry Engine

## Extended Documentation & Engineering Portfolio
For a comprehensive overview of my core engineering competencies, academic design verifications, and cross-disciplinary hardware reports across Electrical, Optical, and Automation domains, access the full live document here:
🔗 **[Read My Full Engineering Portfolio (Google Docs)](https://docs.google.com/document/d/1Tb6pgupiTu2QQavw6dolYQGQl6Y3FALmsouG02qJByU/edit?usp=drive_link)**

---

## Project Overview
This repository hosts the complete, production-grade automated characterization sweep and signal processing framework developed for a **Multi-Instrument Electro-Optical LIV Test Bench**.

The system synchronizes discrete industrial benchtop instruments via an instrumentation bus utilizing the **PyVISA** driver core and the **SCPI Protocol Standard**. The downstream data pipeline acts as an automated metrology framework, integrating vectorized database purification via **Pandas** and high-precision non-linear regression using **SciPy** to calculate laser diode threshold boundaries and monitor silicon wafer material stability.

---

## System Architecture & Concurrent Handshake Topology

The core test executive is engineered around a **Deterministic Event-Driven Tri-Thread Concurrency Framework** built to eliminate race conditions in memory and establish structural hardware isolation.

### 1. Polychromatic Achromatic Doublet Layout & Alignment (Zemax Integration)
To neutralize Longitudinal Chromatic Aberration (LCA) and third-order Spherical Aberration driven by broad visible spectrum illumination (Fraunhofer F, d, C lines), the optical front-end utilizes a custom-optimized multi-element Achromatic Doublet configuration. By pairing a positive low-dispersion Crown element (`N-BK7`) with a negative high-dispersion Flint element (`N-SF11`), opposing dispersion slopes cancel out, compressing the white-light blur circle down to an absolute physical footprint of **RMS: 33.947 µm** at the focal plane.

```text
       Surface 1                   Surface 2 (STOP)            Surface 3
     R = 30.491 mm               R = -28.324 mm              R = -58.711 mm
           │                           │                           │
           ▼                           ▼                           ▼
         ┌───┐                       ┌───┐                         │
        ╱     ╲                     ╱ │ ╱                          │
       │  N-   │                   │  │ │                          │
       │  BK7  │                   │SF│ │                          │
 Input ├───┬───┤   Glued Interface ├──┼─┤                          │
 White ├─> │ ─>├──────────────────>├──┼─┼─────────────────────────>┼─> [ Unified Focus ]
 Light ├───┴───┤   (Cemented)      └──┴─┘                          │   RMS: 33.947 µm
       │ Crown │                     Flint                         │   GEO: 60.504 µm
 (EPD) └───┬───┘                     Aperture                      │       │
 20.0mm    │                           │                           │       ▼
       CT = 6.000 mm               CT = 4.000 mm                   │   Sensor Plane
        ╲     ╱                     ╲ │ ╱                          │      (IMA)
         └───┘                       └───┘                         │       │
           │                           │                           │       ▼
           └──────────┬────────────────┴───────────────────────────┘       │
                      │                                                    │
                      ▼                                                    ▼
              [ Lens 1: Positive ]                                         │
              [ Lens 2: Negative ]                                         │
                      │                                                    │
                      └───────────────── Back Focus Distance ──────────────┘
```

### 2. Automated Emission Controller (Thread 1 - Sourcing Exec)
Gates a **Keithley Source Measure Unit (SMU)** as the master sourcing chassis on a dedicated execution thread. It loops through parametric current injection arrays with local hardware current compliance locked programmatically at **100mA** (`:SOUR:CURR:PROT 0.1`) to guarantee absolute semiconductor fixture protection.

### 3. Optical Telemetry Tracker (Thread 2 - Sensing Exec)
Controls a **Keysight Optical Power Meter** asynchronously. Operating at kernel-level blocked states, this thread consumes 0% CPU overhead while waiting for driver synchronization tokens. It extracts raw power measurements from the instrumentation bus and routes them to a structured volatile results registry in RAM.

### 4. Asynchronous Safety Supervisor (Thread 3 - Thermal Intercept)
An independent high-frequency monitoring loop that continuously queries active system core temperatures. If a critical thermal surge or over-voltage state is detected crossing a hard **45°C cutoff ceiling**, Thread 3 instantly triggers a global **Asynchronous Emergency Interrupt** (`emergency_interrupt.set()`), breaking the active sweep loops and forcing an immediate cascading analog power shutdown (`OUTP OFF`) to secure the hardware.

---

## Hardware Modules & Co-Simulation Data

The project parameters and analytics filters are mathematically aligned with physical device design constraints modeled in standard engineering simulation platforms:

*   **📂 Hardware-Circuit-LTspice:** Houses raw analog `.asc` circuit source files proving electrical lifecycle security. It validates a matted AC-DC half-wave rectifier, a `100µF` smoothing filter to eliminate light source flicker, and a low-side N-channel MOSFET switching driver (`2N7002`) paired with a fast `1N4148` flyback snubber to clamp inductive kickback voltage spikes to a secure `9.7V` plateau.
*   **📂 Optics-Design-Zemax:** Deploys the custom-optimized multi-element **Achromatic Doublet** lens files (`.zmx`). The package is zipped universally as `Project_6_Zemax_Source.zip` to prevent binary MIME-type identification conflicts across cross-platform environments.

---

## Data Analysis & Visual Outputs
Following a safe sweep termination, the telemetry arrays are ingested into a **Pandas DataFrame** for vectorized data purification (`.dropna()`, `.copy()`, and SI unit standardizations to Amperes and Watts). The dataset is then processed via **SciPy** non-linear least-squares optimization (`curve_fit`) to extract the precise device **Slope Efficiency** and standard error parameters directly from the diagonal elements of the **Covariance Matrix** (`pcov`).

The final visualization panel executes deep signal tracing by compiling a synchronized dual-plot layout displaying the master LIV sweep profile alongside an integrated **Residuals Analysis** matrix to detect localized microstructural material failures.

*   **Core Automation Engine:** `smu_liv_sweep_analytics.py`
*   **Pipeline Architecture Layout:** `architecture_flow.txt`
*   **Core Analytics Graphic Output:**

![Laser LIV Characterization Suite](liv_characterization_suite.png)

---

## Technical Stack & Dependencies
*   **Language Environment:** Python 3.x
*   **Driver Interface:** PyVISA / NI-VISA Core Backend
*   **Data Science Infrastructure:** NumPy (Vectorized coordinate matrices), Pandas (Relational structures), SciPy (Least-squares optimization engines)
*   **Visualization Layer:** Matplotlib (LaTeX-integrated vector graphics engine deployed at `dpi=300`)
*   **Communication Protocol Standard:** IEEE-488.2 / SCPI Architecture
*   **Simulation Simulation Environments:** Ansys Zemax OpticStudio & Analog Devices LTspice (v26.0.2)

## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
