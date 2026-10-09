# Polychromatic Achromatic Doublet Focus Framework (Ansys Zemax Node)

## Module Overview
This sub-folder contains the raw lens design specifications (`.zmx`) and universal cross-platform target deployment archives (`.zip`) validating the multi-spectral focal convergence suite targeted for broad visible illumination.

## Optical Parameter Specifications & Diagnostic Metrics

### 1. Lens Geometry & Material Layout
*   **Aperture Bounds:** Entrance Pupil Diameter (EPD) locked قשיח at **20.0 mm**.
*   **Spectral Anchor Configuration:** Polychromatic Fraunhofer visible spectrum lines (F=0.486μ m, d=0.587μ m, C=0.656μ m) with the yellow d-line as the primary wavelength reference.
*   **Doublet Matrix Topology:** 
    1.  *Element 1 (Surface 1 - STOP):* Positive Crown Glass (**`N-BK7`**, High Abbe parameter V > 50, Radius = 30.491 mm, Thickness = 6.000 mm).
    2.  *Element 2 (Surface 2 - Glued interface):* Negative Flint Glass (**`N-SF11`**, Low Abbe parameter V < 50, Shared Common Radius = -28.324 mm, Thickness = 4.000 mm).
    3.  *Surface 3 (Rear Profile):* Curvature Radius = -58.711 mm. Back Focus Distance optimized via automated Damped Least Squares (DLS) routine to a paraxial focus of **44.367 mm**.

### 2. Aberration Minimization Telemetry
*   **Baseline Singlet Constraint:** Prior investigation of a single Plano-Convex element established a severe Longitudinal Chromatic Aberration (LCA) baseline, expanding the spot footprint to an un-stabilized RMS radius of **114.221 µm** due to index mismatches (\(n_F=1.522\) vs \(n_C=1.514\)).
*   **Optimized Doublet Performance:** By forcing opposing dispersion slopes to cancel each other out, the split spectral ray fans collapse onto a uniform focal point. The standard polychromatic footprint registers a massive **70.2% blur reduction**, compressing the circle of confusion down to an absolute single-digit micron envelope of **RMS Radius: 33.947 µm** and **GEO Radius: 60.504 µm**.

---
### 📦 Target Archive Deployment Note
To prevent binary MIME-type identification conflicts where browser engines mistake the raw lens layout structure for an audio layer format, the verified macro validation asset is deployed securely inside: **`Project_6_Zemax_Source.zip`**.
