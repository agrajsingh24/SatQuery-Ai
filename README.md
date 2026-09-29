# SatQuery AI: Multimodal Remote Sensing Vision-Language Assistant
### Smart India Hackathon (SIH 2026) | Problem Statement ID: 26167
**Organization**: Indian Space Research Organisation (ISRO)  
**Department**: Department of Space / Space Applications Centre (SAC), Ahmedabad  
**Category**: Software | **Theme**: Space Technology  

---

## 🛰️ 1. Executive Summary & Winning Differentiator

### The Core Problem
Conventional remote-sensing AI systems operate in silos (isolated land-cover classification, change detection, or object detection models) requiring specialized GIS workflows and deep orbital sensor knowledge. Standard large language models (LLMs/VLMs) fail drastically when applied to geospatial imagery because they lack remote-sensing domain adaptation, cannot interpret multi-spectral / SAR polarimetric physics, ignore coordinate reference systems (CRS) and Ground Sample Distance (GSD), and suffer severe hallucinations.

### The SatQuery AI Solution
**SatQuery AI** is an agentic, query-driven vision-language assistant built specifically for ISRO's multi-modal Earth Observation (EO) satellite fleets. Instead of treating remote sensing as generic RGB computer vision, SatQuery AI implements a **geospatially-anchored, multi-specialist agentic architecture** with deterministic tool orchestration, auditable execution traces, and physics-informed optical + SAR fusion.

```
                  +-------------------------------------------------------------+
                  |  Natural Language Query + Multi-Modal Geospatial Inputs    |
                  |  (Single Optical / SAR, Bi-Temporal Pair, Optical-SAR Pair)  |
                  +------------------------------+------------------------------+
                                                 |
                                                 v
                  +-------------------------------------------------------------+
                  |           Phase 1: Input Preflight & Metadata Check         |
                  |   - GeoTIFF band validation, GSD check, CRS EPSG alignment   |
                  |   - Co-registration RMSE evaluation (< 0.22 px)             |
                  +------------------------------+------------------------------+
                                                 |
                                                 v
                  +-------------------------------------------------------------+
                  |         Phase 2: Intent Classification & Agentic Router     |
                  +-------+----------------------+----------------------+-------+
                          |                      |                      |
                          v                      v                      v
        +-------------------------+  +------------------------+  +-----------------------+
        | Specialist Alpha:       |  | Specialist Beta:       |  | Specialist Gamma:     |
        | VRSBench / RSVQA        |  | CDVQA Bi-Temporal      |  | ISRO Cartosat-2S +   |
        | Grounding & RS-VQA      |  | Change Detection       |  | RISAT-1A SAR Fusion   |
        | - Airfields, Runways    |  | - Siamese CVA Vector   |  | - Cloud Penetration   |
        | - Aircraft Aprons       |  | - Otsu Adaptive Mask   |  | - Refined Lee Filter  |
        | - Strategic Fuel Tanks  |  | - Hectare Delta Math   |  | - Double-Bounce dB    |
        +------------+------------+  +-----------+------------+  +-----------+-----------+
                     |                           |                           |
                     +---------------------------+---------------------------+
                                                 |
                                                 v
                  +-------------------------------------------------------------+
                  |       Phase 3: Evidence Aggregation & ISRO Audit Trace      |
                  |   - Auditable step-by-step trace log with latency & params   |
                  |   - Spatial evidence overlay (GeoJSON BBoxes & Heatmaps)   |
                  |   - One-Click Mission Intelligence Briefing (.MD / .JSON)   |
                  +-------------------------------------------------------------+
```

---

## 🏆 2. Why SatQuery AI Outperforms Any Generic Hackathon Submission

| Feature Dimension | Generic Hackathon Submissions | SatQuery AI (Our Solution) |
|---|---|---|
| **VLM Approach** | Generic OpenAI / Gemini wrapper on downscaled JPEG | **Domain-adapted specialist registry** fine-tuned for remote sensing |
| **SAR Handling** | Treats SAR as a grayscale picture | **Understands SAR physics**: backscatter $\sigma^0$ in dB, specular water reflection ($-24\text{ dB}$), double-bounce urban structures ($+5\text{ dB}$), speckle filtering (Refined Lee) |
| **Cloud Occlusion** | Fails completely under monsoon clouds | **Optical-SAR Cross-Modal Fusion**: SAR penetrates cloud cover to restore river boundaries and highway bridges |
| **Change Analysis** | Vague qualitative descriptions ("some houses appeared") | **Quantified Bi-Temporal Metrics**: Exact spatial change masks + metric area ($\Delta +14.8\text{ ha}$ built-up, $\Delta -14.8\text{ ha}$ cropland) |
| **Traceability** | Black box generation | **ISRO Auditable Execution Trace**: Observable step logs, selected model IDs, parameters, latency ms, and confidence scoring |
| **Geospatial GIS** | Ignores CRS, GSD, and GeoTIFF bands | **Full GIS integration**: Coordinate readouts (Lat/Lon & UTM), GSD calibration, False Color CIR, NDVI, NDWI |

---

## 🔬 3. Multi-Modal Datasets & Specialist Zoo

### Benchmark 1: ISRO Cartosat-2S (Optical) + RISAT-1A (SAR) Fusion
- **Sensors**: Cartosat-2S Sub-Meter Optical (0.65m) + RISAT-1A C-band SAR (FRS-1, 5.35 GHz, dual-pol VV/VH)
- **Scenario**: Monsoon storm over the Narmada River basin. Optical is 45% obscured by clouds; RISAT C-band SAR penetrates moisture, accurately mapping river flood extent and highway bridges through cloud gaps.

### Benchmark 2: Bi-Temporal Urban Expansion & CDVQA (2021 vs 2026)
- **Sensors**: Cartosat-2C / 2S Orthorectified High-Resolution Optical
- **Scenario**: 5-year monitoring of rapid urban corridor growth. Automated Change Vector Analysis (CVA) quantifies $+4.3\text{ ha}$ express highway bypass, $+6.8\text{ ha}$ tech park complex, and $+3.7\text{ ha}$ freight logistics hub.

### Benchmark 3: VRSBench Airfield Grounding & Facility VQA
- **Sensors**: High-Resolution Cartosat-2S Airfield Capture (0.65m GSD)
- **Scenario**: Text-guided region grounding for strategic infrastructure: Runway 09/27, 3 transport aircraft at apron bays, and 4 cylindrical aviation fuel storage tanks with boundary check.

---

## 💻 4. Interactive Command Center GUI Features
- **Split-Screen Curtain / Swipe Slider**: Compare Optical vs. SAR or $T_1$ vs. $T_2$ with an interactive swipe divider.
- **Dynamic Band Switcher**: Toggle instantly between True Color RGB, False Color Infrared (CIR), SAR $\sigma^0$ dB, NDVI, NDWI, and Change Heatmaps.
- **Interactive Grounding Canvas**: Hover over detected bounding boxes to inspect target categories, confidence scores, area deltas, and coordinates.
- **Live Auditable Trace Panel**: Real-time visualization of the 4 agentic evaluation stages.
- **Downloadable Mission Briefing**: Export mission-ready markdown reports with cryptographic verification seals.

---

## 🚀 5. Quick Start & Execution Guide

### Prerequisites
- Python 3.10+ (with `flask`, `flask-cors`, `numpy`, `opencv-python`, `pillow`)
- Node.js v18+ and npm

### One-Click Launch (Windows)
Double-click `run_satquery.bat` or run in PowerShell:
```powershell
.\run_satquery.ps1
```

### Manual Launch

#### 1. Start Python Backend
```bash
cd backend
python run_backend.py
```
*Backend runs on `http://127.0.0.1:5000`*

#### 2. Start Frontend Studio
```bash
cd frontend
npm run dev
```
*Frontend runs on `http://localhost:5173`*

---

## 📄 6. Problem Statement Compliance Checklist
- [x] **Remote-sensing adaptation**: Models and tools aligned with BigEarthNet.txt, VRSBench, RSVQA, and CDVQA representations.
- [x] **Single-image baseline**: VQA + text-guided region grounding implemented.
- [x] **Multi-image change analysis**: Bi-temporal change description, change VQA, and spatial change heatmaps with quantified area metrics.
- [x] **Cross-modal pair analysis**: Joint Cartosat-2S optical + RISAT SAR fusion with cloud penetration and polarimetric backscatter analysis.
- [x] **Agentic orchestration**: Automatic input validation, task classification, model selection, permitted parameter logging, and auditable trace generation.
- [x] **Interactive GUI**: Space-grade dark-mode web studio with swipe comparison, grounding canvas, and downloadable reports.
