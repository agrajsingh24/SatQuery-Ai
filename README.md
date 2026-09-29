# 🛰️ SatQuery AI

### Multimodal Remote Sensing Vision-Language Assistant

**Smart India Hackathon (SIH) 2026**
**Problem Statement ID:** 26167
**Organization:** Indian Space Research Organisation (ISRO)
**Department:** Department of Space / Space Applications Centre (SAC), Ahmedabad
**Category:** Software
**Theme:** Space Technology

---

## 📌 Table of Contents

* [Overview](#-overview)
* [Problem Statement](#-problem-statement)
* [Solution](#-solution)
* [Key Differentiators](#-key-differentiators)
* [System Architecture](#-system-architecture)
* [Multimodal Intelligence](#-multimodal-intelligence)
* [Specialist Model & Dataset Registry](#-specialist-model--dataset-registry)
* [Core Capabilities](#-core-capabilities)
* [Interactive Command Center](#-interactive-command-center)
* [Execution Workflow](#-execution-workflow)
* [Quick Start](#-quick-start)
* [Project Structure](#-project-structure)
* [Problem Statement Compliance](#-problem-statement-compliance)
* [Future Scope](#-future-scope)

---

# 🌍 Overview

**SatQuery AI** is an agentic, query-driven **Vision-Language Assistant for multimodal Earth Observation (EO)**.

It is designed specifically for remote-sensing workflows involving:

* 🛰️ Optical satellite imagery
* 📡 SAR imagery
* 🔄 Bi-temporal image pairs
* 🔗 Optical + SAR multimodal pairs
* 🗺️ Geospatial metadata and coordinate systems
* 🤖 Vision-language question answering
* 🎯 Text-guided object/region grounding
* 📊 Quantitative change detection
* 🔍 Auditable AI inference

Unlike generic computer-vision or LLM-based systems, SatQuery AI treats satellite imagery as **geospatial scientific data**, rather than simply as RGB images.

The system combines domain-specialized vision models, deterministic geospatial processing, agentic task routing, multimodal fusion, and an auditable execution trace into a single interactive workspace.

---

# ❗ Problem Statement

Traditional remote-sensing AI systems are often built as isolated solutions:

* One model for land-cover classification
* Another for object detection
* Another for change detection
* Separate GIS software for spatial analysis
* Separate tools for SAR processing
* Manual workflows for interpreting satellite metadata

This creates several limitations:

### 1. Generic VLM Limitations

General-purpose LLMs and VLMs are not inherently designed to understand:

* Multispectral satellite bands
* SAR backscatter
* Polarimetric information
* Ground Sample Distance (GSD)
* Coordinate Reference Systems (CRS)
* GeoTIFF metadata
* Remote-sensing-specific spatial relationships

### 2. Lack of Multimodal Fusion

Optical imagery can become unreliable under cloud cover, while SAR provides complementary information but requires different processing and interpretation.

### 3. Limited Quantification

Many systems produce qualitative descriptions such as:

> "Some buildings appear to have been constructed."

SatQuery AI instead aims to produce spatially grounded and measurable outputs such as:

* Change masks
* Area deltas
* Object coordinates
* Confidence values
* Spatial overlays

### 4. Limited Explainability

Black-box AI inference makes it difficult to understand:

* Which model was selected
* Which processing operations were executed
* Which parameters were used
* How long each stage took
* What evidence supported the final answer

---

# 💡 Solution

SatQuery AI introduces a **geospatially anchored, multi-specialist agentic architecture** for remote-sensing intelligence.

The system accepts a natural-language query together with one or more geospatial inputs and automatically determines the appropriate analysis workflow.

### Supported Input Modes

| Input Mode                           | Example Use Case                               |
| ------------------------------------ | ---------------------------------------------- |
| **Single Optical Image**             | Object detection, VQA, facility identification |
| **Single SAR Image**                 | SAR interpretation and target analysis         |
| **Bi-Temporal Pair**                 | Urban expansion and land-use change            |
| **Optical + SAR Pair**               | Cloud-resilient multimodal analysis            |
| **Natural Language Query + Imagery** | Grounded question answering                    |

---

# ⭐ Key Differentiators

| Capability                | Conventional / Generic Approach | SatQuery AI                                           |
| ------------------------- | ------------------------------- | ----------------------------------------------------- |
| **Vision-Language Model** | Generic VLM applied to image    | Domain-specialized remote-sensing model registry      |
| **SAR Analysis**          | Treat SAR as grayscale imagery  | SAR-aware backscatter and speckle-processing pipeline |
| **Cloud Occlusion**       | Optical-only analysis           | Optical + SAR cross-modal fusion                      |
| **Change Detection**      | Qualitative descriptions        | Spatial masks + quantified area change                |
| **Geospatial Context**    | Often ignored                   | CRS, GSD, coordinates and GeoTIFF metadata            |
| **Model Selection**       | Manually selected models        | Agentic task classification and routing               |
| **Traceability**          | Black-box inference             | Step-by-step execution trace                          |
| **Evidence**              | Text-only response              | Spatial overlays, bounding boxes and heatmaps         |
| **Reporting**             | Manual documentation            | Exportable mission intelligence briefing              |

---

# 🏗️ System Architecture

```text
┌──────────────────────────────────────────────────────────────────────┐
│                 NATURAL LANGUAGE QUERY + EO INPUTS                   │
│                                                                      │
│   Optical Image │ SAR │ Bi-Temporal Pair │ Optical + SAR Pair       │
└───────────────────────────────┬──────────────────────────────────────┘
                                │
                                ▼
┌──────────────────────────────────────────────────────────────────────┐
│                    PHASE 1 — INPUT PREFLIGHT                        │
│                                                                      │
│  • GeoTIFF / band validation                                        │
│  • CRS / EPSG validation                                            │
│  • GSD verification                                                 │
│  • Image metadata inspection                                        │
│  • Co-registration quality assessment                               │
└───────────────────────────────┬──────────────────────────────────────┘
                                │
                                ▼
┌──────────────────────────────────────────────────────────────────────┐
│                PHASE 2 — INTENT CLASSIFICATION                      │
│                     & AGENTIC ROUTING                               │
└───────────────┬──────────────────┬──────────────────┬───────────────┘
                │                  │                  │
                ▼                  ▼                  ▼
┌──────────────────────┐ ┌──────────────────────┐ ┌──────────────────────┐
│ SPECIALIST ALPHA     │ │ SPECIALIST BETA      │ │ SPECIALIST GAMMA     │
│                      │ │                      │ │                      │
│ VRSBench / RSVQA     │ │ CDVQA / Change       │ │ Optical + SAR        │
│ Grounding & RS-VQA   │ │ Detection            │ │ Fusion               │
│                      │ │                      │ │                      │
│ • Airfields          │ │ • Change vectors     │ │ • Cloud penetration  │
│ • Runways            │ │ • Change masks       │ │ • SAR processing     │
│ • Aircraft           │ │ • Area calculations  │ │ • Backscatter        │
│ • Fuel facilities    │ │ • Bi-temporal VQA    │ │ • Multimodal fusion  │
└───────────┬──────────┘ └───────────┬──────────┘ └───────────┬──────────┘
            │                        │                        │
            └────────────────────────┼────────────────────────┘
                                     │
                                     ▼
┌──────────────────────────────────────────────────────────────────────┐
│             PHASE 3 — EVIDENCE AGGREGATION                          │
│                                                                      │
│  • Model outputs                                                    │
│  • Spatial evidence                                                 │
│  • Confidence values                                                │
│  • Change metrics                                                   │
│  • Coordinates / bounding boxes                                     │
└───────────────────────────────┬──────────────────────────────────────┘
                                │
                                ▼
┌──────────────────────────────────────────────────────────────────────┐
│                PHASE 4 — AUDIT & MISSION REPORTING                  │
│                                                                      │
│  • Execution trace                                                  │
│  • Processing parameters                                            │
│  • Model identifiers                                                │
│  • Latency measurements                                             │
│  • GeoJSON / heatmap overlays                                       │
│  • Mission intelligence briefing                                    │
└──────────────────────────────────────────────────────────────────────┘
```

---

# 🔬 Multimodal Intelligence

SatQuery AI is designed around three major analysis pathways.

## 1. Optical Remote Sensing

Optical imagery can support:

* Object identification
* Scene understanding
* Remote-sensing VQA
* Region grounding
* Infrastructure analysis
* Spectral index generation

Supported visualization products include:

* True Color RGB
* False Color Infrared (CIR)
* NDVI
* NDWI

---

## 2. SAR Intelligence

Synthetic Aperture Radar provides complementary information when optical imagery is affected by:

* Cloud cover
* Haze
* Atmospheric conditions
* Low-light conditions

The SAR processing pipeline can incorporate:

* Backscatter analysis
* $\sigma^0$ representation
* dB visualization
* Speckle reduction
* Refined Lee filtering
* Double-bounce interpretation
* Polarimetric information such as VV/VH

---

## 3. Optical + SAR Fusion

SatQuery AI combines complementary information from optical and SAR observations.

```text
             OPTICAL                         SAR
                │                             │
                │                             │
       ┌────────▼────────┐           ┌────────▼────────┐
       │ Spectral /      │           │ Backscatter /   │
       │ Visual Features│           │ Structural Info │
       └────────┬────────┘           └────────┬────────┘
                │                             │
                └──────────────┬──────────────┘
                               ▼
                     ┌────────────────────┐
                     │ Multimodal Fusion  │
                     └─────────┬──────────┘
                               ▼
                     ┌────────────────────┐
                     │ Grounded Analysis  │
                     └────────────────────┘
```

This enables analysis of scenes where optical imagery alone may provide incomplete information.

---

# 🧠 Specialist Model & Dataset Registry

SatQuery AI organizes remote-sensing intelligence into specialized model/data capabilities rather than relying on a single generic VLM.

## Benchmark 1 — Optical + SAR Fusion

**Sensors**

* Cartosat-2S optical imagery
* RISAT-1A C-band SAR
* FRS-1 configuration
* VV/VH polarization

**Scenario**

A monsoon-affected region where cloud cover limits optical visibility.

The multimodal pipeline combines optical information with SAR observations to analyze features such as:

* River boundaries
* Flood extent
* Roads
* Bridges
* Urban structures

---

## Benchmark 2 — Bi-Temporal Urban Expansion

**Sensors**

* Cartosat-2C / Cartosat-2S
* Orthorectified high-resolution optical imagery

**Scenario**

Comparison of satellite observations across multiple years to identify urban expansion.

Potential outputs include:

* Change vectors
* Spatial change masks
* Built-up area change
* Infrastructure expansion
* Area statistics
* Change heatmaps

Example quantified outputs:

```text
Expressway bypass       → +4.3 ha
Technology park         → +6.8 ha
Freight logistics hub   → +3.7 ha
```

---

## Benchmark 3 — VRSBench / RS-VQA Grounding

**Scenario**

High-resolution airfield imagery used for text-guided region grounding and visual question answering.

Example targets:

* Runways
* Aircraft
* Aircraft aprons
* Fuel storage facilities
* Other infrastructure

The system associates detected regions with:

* Target category
* Confidence
* Spatial coordinates
* Bounding geometry

---

# 🖥️ Interactive Command Center

SatQuery AI provides a web-based command center for exploring model outputs and geospatial evidence.

## 🌓 Split-Screen Comparison

Interactive swipe/curtain comparison for:

* Optical vs. SAR
* Time $T_1$ vs. Time $T_2$
* Original vs. processed imagery
* Input vs. detected change

---

## 🎨 Dynamic Visualization Layers

Users can switch between:

```text
RGB
│
├── True Color
├── False Color / CIR
├── NDVI
├── NDWI
├── SAR σ⁰ / dB
└── Change Heatmap
```

---

## 🎯 Interactive Grounding Canvas

Detected objects and regions can be inspected directly on the image.

Each grounded region can expose:
