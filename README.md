# 🏛️ HeritageGuard

## AI-Assisted Heritage Conservation Decision Intelligence Platform

> **From detecting heritage damage to deciding what should be preserved first.**

HeritageGuard is an AI-assisted decision-support platform designed for heritage authorities, archaeology departments, museums, cultural institutions and heritage organizations.

The system combines:

* Computer vision-based heritage damage detection
* Asset condition assessment
* Deterioration and risk analysis
* Cultural significance
* Environmental risk
* Intervention cost
* Resource constraints
* Portfolio optimization
* Explainable recommendations
* Budget and intervention what-if simulation

The core objective is not simply to identify damage, but to determine **which assets should be conserved first, which intervention should be performed, and how limited resources should be allocated for maximum preservation benefit**.

---

# 📌 Table of Contents

* [1. Problem Statement](#1-problem-statement)
* [2. Proposed Solution](#2-proposed-solution)
* [3. Core Innovation](#3-core-innovation)
* [4. System Architecture](#4-system-architecture)
* [5. End-to-End Workflow](#5-end-to-end-workflow)
* [6. Computer Vision Module](#6-computer-vision-module)
* [7. Dataset](#7-dataset)
* [8. YOLO Dataset Structure](#8-yolo-dataset-structure)
* [9. YOLO Training Pipeline](#9-yolo-training-pipeline)
* [10. Damage Detection Classes](#10-damage-detection-classes)
* [11. Condition Scoring](#11-condition-scoring)
* [12. Deterioration and Risk Analysis](#12-deterioration-and-risk-analysis)
* [13. Conservation Optimization](#13-conservation-optimization)
* [14. Explainability](#14-explainability)
* [15. What-If Simulation](#15-what-if-simulation)
* [16. Technology Stack](#16-technology-stack)
* [17. Backend Architecture](#17-backend-architecture)
* [18. Database Architecture](#18-database-architecture)
* [19. GIS Layer](#19-gis-layer)
* [20. Frontend / Dashboard](#20-frontend--dashboard)
* [21. API Architecture](#21-api-architecture)
* [22. Deployment Architecture](#22-deployment-architecture)
* [23. Repository Structure](#23-repository-structure)
* [24. Current Prototype vs Planned System](#24-current-prototype-vs-planned-system)
* [25. Security](#25-security)
* [26. Scalability](#26-scalability)
* [27. Risks and Mitigation](#27-risks-and-mitigation)
* [28. Competitive Differentiation](#28-competitive-differentiation)
* [29. Limitations](#29-limitations)
* [30. Future Scope](#30-future-scope)
* [31. Development Roadmap](#31-development-roadmap)
* [32. Technical Interview / Judge Questions](#32-technical-interview--judge-questions)
* [33. Dataset Licensing](#33-dataset-licensing)
* [34. Team](#34-team)

---

# 1. Problem Statement

Heritage organizations manage large portfolios of monuments and cultural assets while dealing with limited:

* Conservation budgets
* Skilled personnel
* Inspection time
* Restoration capacity
* Historical and condition data

The problem is therefore not only:

> **"Can we detect damage?"**

The more important question is:

> **"Given limited resources, which heritage assets should be conserved first, what intervention should be performed, and how should resources be allocated?"**

Traditional workflows often involve inspection, documentation, GIS, condition assessment and expert judgement. These processes are valuable but can become fragmented when managing large portfolios.

---

# 2. Proposed Solution

HeritageGuard combines computer vision, structured heritage data, GIS and optimization into a single conservation decision-support workflow.

### Input

The system can use:

* Heritage images
* Historical condition records
* GIS/location information
* Cultural significance
* Environmental risk
* Intervention options
* Intervention cost
* Available budget
* Available manpower
* Time constraints

### Processing

```text
Images
   ↓
AI Damage Detection
   ↓
Condition Assessment
   ↓
Deterioration Analysis
   ↓
Risk Analysis
   ↓
Intervention Alternatives
   ↓
Cost + Preservation Benefit
   ↓
Portfolio Optimization
   ↓
Explainable Recommendation
   ↓
What-If Simulation
```

### Output

The system provides:

* Priority assets
* Detected damage
* Estimated condition
* Risk indicators
* Recommended interventions
* Expected preservation benefit
* Resource requirements
* Budget allocation
* Explanation for each recommendation
* Alternative plans under different constraints

---

# 3. Core Innovation

HeritageGuard is not positioned as simply another heritage inventory, GIS or damage-detection system.

The central innovation is the **decision layer**.

Existing systems often answer:

> **"Where is the heritage asset and what is its condition?"**

HeritageGuard aims to answer:

> **"Given limited resources, what should we preserve first, what should we do, and what happens if our constraints change?"**

The proposed differentiators are:

1. Portfolio-level optimization
2. Budget-constrained intervention planning
3. Integration of damage evidence with cultural significance and risk
4. Intervention selection
5. Explainable recommendations
6. What-if simulation
7. Longitudinal condition tracking
8. Human-in-the-loop conservation decisions

---

# 4. System Architecture

```text
                         HERITAGEGUARD
                              │
              ┌───────────────┴────────────────┐
              │                                │
        DATA INGESTION                    USER INPUT
              │                                │
     ┌────────┼────────┐                       │
     │        │        │                       │
  Images     GIS   Historical Data        Budget/Resources
     │        │        │                       │
     └────────┴────────┴──────────────┬────────┘
                                      │
                                      ▼
                           ┌────────────────────┐
                           │ Computer Vision     │
                           │ YOLO Damage Model   │
                           └─────────┬──────────┘
                                     │
                                     ▼
                           Damage / Condition
                                     │
                                     ▼
                         ┌──────────────────────┐
                         │ Risk & Deterioration │
                         │ Analysis             │
                         └──────────┬───────────┘
                                    │
                                    ▼
                         ┌──────────────────────┐
                         │ Intervention Engine  │
                         └──────────┬───────────┘
                                    │
                                    ▼
                         ┌──────────────────────┐
                         │ Optimization Engine  │
                         │ Budget + Resources   │
                         └──────────┬───────────┘
                                    │
                                    ▼
                         ┌──────────────────────┐
                         │ Explainability       │
                         │ + What-If Engine     │
                         └──────────┬───────────┘
                                    │
                                    ▼
                         ┌──────────────────────┐
                         │ Web Dashboard        │
                         │ Maps + Analytics     │
                         └──────────────────────┘
```

---

# 5. End-to-End Workflow

## Step 1 — Asset Registration

Each heritage asset receives a unique identifier.

Example:

```text
asset_id: HG-0001
monument_name: Example Heritage Structure
location: latitude, longitude
heritage_type: Monument
historical_period: 18th Century
material: Stone Masonry
```

---

## Step 2 — Image Collection

Images can come from:

* Ground photography
* Mobile devices
* Professional cameras
* Drone/UAV imagery in future extensions

---

## Step 3 — Damage Detection

The YOLO-based computer vision model detects visible deterioration.

Example:

```text
Input Image
     ↓
YOLO
     ↓
┌─────────────────────────────┐
│ Crack       0.91            │
│ Material Loss 0.84          │
│ Moss        0.76            │
└─────────────────────────────┘
```

The model produces bounding boxes, class labels and confidence scores.

---

## Step 4 — Condition Assessment

Detection results are converted into structured condition indicators.

Possible features include:

* Number of detected damage instances
* Damage type
* Confidence
* Relative affected area
* Severity
* Distribution
* Historical trend

---

## Step 5 — Deterioration Analysis

Historical inspections can be compared to identify whether an asset is:

* Stable
* Improving
* Slowly deteriorating
* Rapidly deteriorating

Example:

```text
2024 → Condition = 78
2025 → Condition = 69
2026 → Condition = 54

Deterioration = increasing
```

---

## Step 6 — Risk Analysis

Risk can combine:

```text
Physical Condition
        +
Deterioration Rate
        +
Environmental Exposure
        +
Cultural Significance
        +
Urgency
```

---

## Step 7 — Intervention Selection

Possible interventions may include:

* Crack repair
* Surface treatment
* Vegetation removal
* Drainage work
* Material restoration
* Structural restoration

---

## Step 8 — Portfolio Optimization

Instead of independently ranking every monument, HeritageGuard selects a **combination of interventions** that provides the highest expected preservation benefit under available constraints.

---

## Step 9 — Explainable Recommendation

Example:

```text
Priority: HIGH

Reasons:
✓ Rapid deterioration
✓ High cultural significance
✓ High environmental exposure
✓ High expected preservation benefit
✓ Intervention is feasible within current budget
```

---

## Step 10 — What-If Simulation

The authority can simulate:

```text
Budget = ₹10,00,000
       ↓
Recommended Portfolio
```

Then:

```text
Budget reduced by 20%
       ↓
Recalculate
       ↓
New Recommended Portfolio
```

---

# 6. Computer Vision Module

The first computer-vision component uses a YOLO-style object detection pipeline.

### Objective

Detect visible heritage deterioration from images.

### Detection Output

Each prediction contains:

```text
class_id
confidence
x_center
y_center
width
height
```

Normalized YOLO coordinates are used in label files.

---

# 7. Dataset

## Primary Dataset — MSD-Det

MSD-Det is used as the primary computer-vision dataset.

Dataset characteristics:

* **1,082 high-resolution images**
* **8,739 annotated damage objects**
* Multi-class heritage masonry damage
* Designed for heritage damage detection

Damage categories include:

1. Cracks
2. Fabric / material loss
3. Surface dissolution
4. Efflorescence
5. Discoloration
6. Plants
7. Moss

The dataset is intended to train and evaluate the main multi-class heritage-damage detection model.

---

# 8. YOLO Dataset Structure

The repository follows the standard YOLO dataset organization.

```text
HeritageGuard-YOLO-Dataset/
│
├── data.yaml
├── .gitattributes
│
├── images/
│   ├── train/
│   ├── val/
│   └── test/
│
├── labels/
│   ├── train/
│   ├── val/
│   └── test/
│
└── README.md
```

### Image directory

Contains the actual heritage photographs.

```text
images/train/
images/val/
images/test/
```

### Label directory

Contains corresponding YOLO annotation files.

```text
labels/train/
labels/val/
labels/test/
```

Every image should have a corresponding label file with the same base filename.

Example:

```text
images/train/image001.jpg
labels/train/image001.txt
```

---

# 9. YOLO Training Pipeline

Recommended workflow:

```text
Dataset
   ↓
Data Validation
   ↓
Train / Validation / Test Split
   ↓
YOLO Configuration
   ↓
Model Training
   ↓
Validation
   ↓
Evaluation
   ↓
Best Model
   ↓
Inference
```

### Typical training process

```bash
pip install ultralytics
```

Then:

```python
from ultralytics import YOLO

model = YOLO("yolo11n.pt")

model.train(
    data="data.yaml",
    epochs=100,
    imgsz=640,
    batch=16
)
```

> The exact YOLO model variant, epochs, image size and batch size should be selected experimentally according to GPU memory and validation performance.

---

# 10. Damage Detection Classes

The primary dataset contains seven heritage-damage categories:

| Class | Damage Type            |
| ----: | ---------------------- |
|     0 | Cracks                 |
|     1 | Fabric / Material Loss |
|     2 | Surface Dissolution    |
|     3 | Efflorescence          |
|     4 | Discoloration          |
|     5 | Plants                 |
|     6 | Moss                   |

The exact numeric mapping must always be taken from the repository's `data.yaml`.

---

# 11. Condition Scoring

The YOLO model does not directly produce a final conservation priority.

It produces visual evidence.

The next layer converts that evidence into condition indicators.

Conceptually:

```text
Damage Detection
      ↓
Damage Type
      ↓
Damage Count
      ↓
Affected Area
      ↓
Confidence
      ↓
Condition Indicators
```

A future condition score can combine multiple normalized factors.

Example conceptual formulation:

```text
Condition Score =
w1 × Damage Severity
+
w2 × Damage Extent
+
w3 × Deterioration Rate
+
w4 × Environmental Risk
```

The weights should be validated with conservation experts rather than treated as universal constants.

---

# 12. Deterioration and Risk Analysis

HeritageGuard should maintain historical observations for each asset.

Example:

```text
Asset: HG-0001

Date       Condition
--------------------
2024       82
2025       71
2026       55
```

The system can estimate deterioration trends.

Possible risk factors:

* Current condition
* Deterioration rate
* Environmental exposure
* Cultural significance
* Urgency
* Damage severity
* Intervention feasibility

The system should provide confidence indicators because computer vision predictions are not perfect.

---

# 13. Conservation Optimization

This is the core decision-intelligence component.

The optimization engine receives:

```text
Assets
+
Interventions
+
Costs
+
Expected preservation benefit
+
Risk
+
Cultural significance
+
Budget
+
Manpower
+
Time constraints
```

### Example

Suppose:

```text
Available budget = ₹10 lakh
```

Possible interventions:

| Asset | Intervention       | Cost | Expected Benefit |
| ----- | ------------------ | ---: | ---------------: |
| A     | Crack Repair       |  ₹3L |             0.90 |
| B     | Surface Treatment  |  ₹2L |             0.50 |
| C     | Structural Repair  |  ₹7L |             0.95 |
| D     | Vegetation Removal |  ₹1L |             0.30 |

The optimization engine chooses the combination that maximizes preservation benefit while satisfying the constraints.

---

## Optimization Concept

A simplified objective can be represented as:

```text
Maximize:

Σ PreservationBenefit(i,j) × Decision(i,j)
```

subject to:

```text
Σ Cost(i,j) × Decision(i,j) ≤ AvailableBudget
```

plus:

```text
Manpower constraints
Time constraints
Intervention dependencies
Asset-specific constraints
```

The exact optimization model will evolve during development.

---

# 14. Explainability

The system should not simply return:

```text
Priority = 92
```

Instead:

```text
Priority = HIGH

Why?

• Rapid deterioration
• High cultural significance
• High environmental risk
• Severe visible damage
• High expected preservation benefit
• Intervention fits available resources
```

This makes the system suitable for expert decision-support.

---

# 15. What-If Simulation

The system can run the optimization engine repeatedly under different constraints.

### Example

#### Scenario A

```text
Budget = ₹20 lakh
```

Output:

```text
Assets A, B, C, D
```

#### Scenario B

```text
Budget = ₹15 lakh
```

Output:

```text
Assets A, C, D
```

#### Scenario C

```text
Asset C intervention delayed
```

Output:

```text
Risk increases
New intervention portfolio generated
```

This allows authorities to compare possible conservation strategies before committing resources.

---

# 16. Technology Stack

## AI / Machine Learning

```text
Python
YOLO
Computer Vision
PyTorch-based deep learning ecosystem
NumPy
Pandas
OpenCV
```

The specific YOLO implementation and model version should be recorded in the training configuration when finalized.

---

## Backend

Recommended:

```text
Python
FastAPI
Pydantic
REST API
```

FastAPI can expose services such as:

```text
POST /api/detection
GET  /api/assets
GET  /api/assets/{id}
POST /api/optimization
POST /api/simulation
GET  /api/recommendations
```

---

## Database

```text
PostgreSQL
PostGIS
```

PostgreSQL stores structured application data while PostGIS enables geospatial queries.

---

## Optimization

Recommended:

```text
Google OR-Tools
```

OR-Tools can be used for budget-constrained portfolio optimization and resource allocation.

---

## GIS

```text
PostGIS
GeoJSON
Web Map
```

Potential map features:

* Heritage asset locations
* Condition indicators
* Risk levels
* Priority levels
* Intervention status

---

## Frontend

A web dashboard can be implemented using:

```text
React
JavaScript / TypeScript
HTML
CSS
Mapping library
Charts / visualization library
```

The final frontend framework should be documented once implementation is finalized.

---

## API / Integration

```text
REST APIs
JSON
Authentication
Data Import / Export
```

---

## Version Control

```text
Git
GitHub
Git LFS
```

Git LFS is used for large image files in the dataset repository.

---

## Deployment

Potential production architecture:

```text
Cloud Infrastructure
        │
        ├── Frontend
        │
        ├── Backend API
        │
        ├── ML Inference Service
        │
        ├── PostgreSQL + PostGIS
        │
        └── Object Storage
```

---

# 17. Backend Architecture

A modular backend can be organized as:

```text
backend/
│
├── api/
│   ├── routes/
│   └── dependencies/
│
├── models/
│
├── schemas/
│
├── services/
│   ├── detection/
│   ├── condition/
│   ├── risk/
│   ├── optimization/
│   └── simulation/
│
├── database/
│
├── utils/
│
└── main.py
```

### Separation of concerns

```text
API
 ↓
Service Layer
 ↓
Business Logic
 ↓
Database / ML / Optimization
```

This makes individual components easier to test and replace.

---

# 18. Database Architecture

Possible core tables:

```text
assets
inspections
damage_detections
condition_scores
risk_assessments
interventions
intervention_costs
optimization_runs
recommendations
users
```

### Example asset record

```text
asset_id
name
location
heritage_type
historical_period
material
cultural_significance
protection_status
```

### Example inspection record

```text
inspection_id
asset_id
inspection_date
image_reference
condition_score
model_confidence
```

### Example intervention record

```text
intervention_id
asset_id
intervention_type
estimated_cost
expected_risk_reduction
expected_preservation_benefit
duration
required_manpower
```

---

# 19. GIS Layer

Each heritage asset can be associated with geographic coordinates.

Example:

```json
{
  "asset_id": "HG-0001",
  "latitude": 12.9716,
  "longitude": 77.5946
}
```

GIS functionality can provide:

* Asset mapping
* Spatial filtering
* Risk visualization
* Regional analysis
* Cluster detection
* Inspection planning

PostGIS can perform spatial queries directly inside PostgreSQL.

---

# 20. Frontend / Dashboard

The dashboard should provide several views.

### 1. Heritage Map

Displays:

```text
Asset Location
Condition
Risk
Priority
Intervention Status
```

### 2. Asset Dashboard

Shows:

```text
Asset Information
Latest Images
Detected Damage
Condition History
Risk
Recommended Intervention
```

### 3. Portfolio Dashboard

Shows:

```text
Total Assets
High-Risk Assets
Available Budget
Recommended Budget Allocation
Expected Preservation Benefit
```

### 4. What-If Dashboard

Allows the user to modify:

```text
Budget
Manpower
Timeline
Intervention delays
```

and rerun the optimization.

---

# 21. API Architecture

Example API flow:

```text
Frontend
   │
   ▼
FastAPI
   │
   ├── Asset Service
   │
   ├── Detection Service
   │
   ├── Risk Service
   │
   ├── Optimization Service
   │
   └── Simulation Service
           │
           ▼
     PostgreSQL/PostGIS
```

### Example

```http
POST /api/detection
```

Input:

```json
{
  "asset_id": "HG-0001",
  "image_url": "..."
}
```

Output:

```json
{
  "asset_id": "HG-0001",
  "detections": [
    {
      "class": "crack",
      "confidence": 0.91,
      "bbox": [0.42, 0.35, 0.18, 0.22]
    }
  ]
}
```

---

# 22. Deployment Architecture

A production deployment can use:

```text
                    Internet
                       │
                       ▼
                Web Application
                       │
                       ▼
                  API Gateway
                       │
            ┌──────────┴──────────┐
            │                     │
       Backend API          ML Inference
            │                     │
            └──────────┬──────────┘
                       │
                 PostgreSQL
                    + PostGIS
                       │
                 Object Storage
```

For the hackathon prototype, the architecture can remain simpler.

The MVP can begin as a software-only system using photographs, existing records and GIS data, with advanced integrations added later.

---

# 23. Repository Structure

The overall project can eventually use:

```text
HeritageGuard/
│
├── frontend/
│
├── backend/
│
├── ml/
│   ├── training/
│   ├── inference/
│   ├── evaluation/
│   └── models/
│
├── optimization/
│
├── database/
│
├── data/
│
├── docs/
│
├── scripts/
│
├── tests/
│
├── docker/
│
├── .env.example
├── docker-compose.yml
├── requirements.txt
└── README.md
```

The current dataset repository is intentionally focused on the YOLO training dataset.

---

# 24. Current Prototype vs Planned System

It is important to distinguish implemented functionality from planned architecture.

## Currently Available

```text
✓ Heritage damage dataset
✓ YOLO-format annotations
✓ Train/validation/test organization
✓ data.yaml
✓ Git repository
✓ Git LFS for large image files
✓ Dataset prepared for YOLO training
```

## In Development / Next

```text
→ YOLO model training
→ Model evaluation
→ Inference pipeline
→ Condition scoring
→ Structured heritage asset dataset
→ Risk analysis
→ OR-Tools optimization
→ Backend API
→ Dashboard
```

## Future

```text
→ GIS integration
→ Historical condition tracking
→ What-if simulation
→ Drone imagery
→ Environmental risk integration
→ Government system integration
→ Production deployment
```

Do not describe future components as already implemented until they have been developed and tested.

---

# 25. Security

A production deployment should include:

### Authentication

```text
JWT / OAuth2
```

### Authorization

Role-based access control:

```text
Admin
Conservation Expert
Inspector
Government Officer
Viewer
```

### Data Security

* HTTPS
* Encrypted database connections
* Secure object storage
* Environment variables for secrets
* No API keys committed to Git
* Input validation
* Audit logs

Sensitive heritage-location data may require restricted access depending on the institution and asset.

---

# 26. Scalability

The architecture is designed to scale from:

```text
10 assets
```

to:

```text
50 assets
```

and eventually:

```text
100s / 1000s of assets
```

Possible scaling strategy:

```text
Frontend
   ↓
Load Balancer
   ↓
Multiple API Instances
   ↓
ML Inference Workers
   ↓
PostgreSQL/PostGIS
   ↓
Object Storage
```

Heavy AI inference can be separated from the main API server.

---

# 27. Risks and Mitigation

| Risk                        | Mitigation                                  |
| --------------------------- | ------------------------------------------- |
| Limited heritage data       | Human-in-the-loop validation                |
| Dataset bias                | External validation datasets                |
| False AI detections         | Confidence thresholds + expert verification |
| Different expert opinions   | Explainable decision factors                |
| Synthetic optimization data | Clearly label synthetic prototype data      |
| Large image storage         | Git LFS / object storage                    |
| Model overconfidence        | Confidence-aware recommendations            |
| Integration complexity      | Modular API/data-import architecture        |
| Incorrect recommendations   | Human approval before operational decisions |

The system is intended as **decision-support for conservation experts, not a replacement for them**.

---

# 28. Competitive Differentiation

HeritageGuard acknowledges existing alternatives.

### Arches

Strong in:

* Heritage inventory
* Data management
* GIS
* Heritage workflows

### GIS Platforms

Strong in:

* Mapping
* Spatial analysis
* Asset management

### AI Inspection Systems

Strong in:

* Automated damage detection
* Computer vision
* Condition inspection

### Traditional Conservation Consultants

Strong in:

* Expert judgement
* Condition assessment
* Conservation planning
* Restoration planning

### HeritageGuard

The proposed differentiation is the integration:

```text
Damage Evidence
      ↓
Deterioration
      ↓
Risk
      ↓
Cultural Significance
      ↓
Intervention
      ↓
Cost
      ↓
Optimization
      ↓
Recommended Portfolio
      ↓
What-If Simulation
```

The project should **not** claim to be the first AI heritage platform.

The defensible positioning is:

> **Existing solutions largely focus on heritage inventory, GIS, documentation, inspection or individual damage detection. HeritageGuard focuses on the decision layer connecting these evidence sources to intervention selection and portfolio-level resource optimization.**

---

# 29. Limitations

Current limitations include:

1. Public computer-vision datasets do not contain all information required for conservation portfolio optimization.
2. Historical condition data may be limited.
3. Intervention cost data may initially be synthetic.
4. Cultural significance requires a transparent expert-defined scoring framework.
5. Environmental risk requires additional data sources.
6. AI predictions can contain false positives and false negatives.
7. The optimization model depends on the quality of input data.
8. Real-world deployment requires expert validation.

The initial POC can therefore use a small structured dataset of approximately 5–10 heritage assets to demonstrate the complete decision pipeline.

---

# 30. Future Scope

### Computer Vision

* Improved YOLO models
* Segmentation
* Crack severity estimation
* Damage-area estimation
* Temporal damage comparison
* Drone imagery
* Multi-modal inspection

### AI

* Deterioration prediction
* Risk forecasting
* Anomaly detection
* Explainable AI
* Expert feedback loops

### Optimization

* Multi-year planning
* Dynamic budget allocation
* Intervention scheduling
* Manpower optimization
* Multi-objective optimization
* Uncertainty-aware optimization

### GIS

* Spatial risk analysis
* Heritage clusters
* Environmental layers
* Inspection route planning

### Platform

* Government integrations
* Mobile inspection application
* Offline field inspection
* Automated reports
* Role-based dashboards
* Multi-organization deployment

---

# 31. Development Roadmap

## Phase 1 — Computer Vision Prototype

```text
Dataset
  ↓
YOLO Training
  ↓
Evaluation
  ↓
Inference
```

## Phase 2 — Asset Intelligence

```text
Asset Registry
  ↓
Condition Scores
  ↓
Historical Records
  ↓
Deterioration Analysis
```

## Phase 3 — Optimization

```text
Interventions
  ↓
Cost
  ↓
Risk
  ↓
Preservation Benefit
  ↓
OR-Tools
  ↓
Recommended Portfolio
```

## Phase 4 — Decision Dashboard

```text
Map
+
Asset Dashboard
+
Recommendations
+
What-If Simulation
```

## Phase 5 — Pilot

Pilot target:

```text
10–50 heritage assets
```

with expert validation.

## Phase 6 — Scale

Deployment for:

* Government heritage authorities
* Archaeology departments
* Museums
* Heritage organizations

---

# 32. Technical Interview / Judge Questions

## Q1. Why YOLO?

YOLO is suitable because the problem requires detecting multiple visible damage types in an image while providing spatial localization.

It produces:

```text
Class
+
Confidence
+
Bounding Box
```

which can then be used by the condition-assessment layer.

---

## Q2. Is YOLO the complete HeritageGuard solution?

**No.**

YOLO is only the computer-vision component.

The complete system is:

```text
YOLO
 ↓
Condition Assessment
 ↓
Risk/Deterioration
 ↓
Intervention Selection
 ↓
Optimization
 ↓
Decision Support
```

The main innovation lies in the decision layer.

---

## Q3. Why not just use the YOLO confidence score as priority?

Because model confidence represents the model's confidence in a visual detection.

It does not represent:

* Cultural significance
* Deterioration rate
* Environmental risk
* Intervention cost
* Expected preservation benefit
* Available budget

Therefore:

```text
AI Confidence ≠ Conservation Priority
```

---

## Q4. How is the final priority calculated?

The proposed system combines multiple factors:

```text
Condition
+
Deterioration
+
Cultural Significance
+
Environmental Risk
+
Urgency
+
Intervention Cost
+
Expected Preservation Benefit
+
Resource Constraints
```

The final decision is produced through an optimization process rather than a single arbitrary score.

---

## Q5. Why use OR-Tools?

Because the problem is fundamentally a constrained resource-allocation problem.

OR-Tools can model:

* Budget constraints
* Manpower constraints
* Scheduling
* Intervention dependencies
* Portfolio selection

---

## Q6. Why PostgreSQL + PostGIS?

PostgreSQL provides reliable structured data storage.

PostGIS adds geospatial capabilities required for:

* Heritage coordinates
* Spatial queries
* GIS analysis
* Geographic filtering
* Mapping

---

## Q7. Why not use MongoDB?

MongoDB could technically be used, but PostgreSQL + PostGIS is a better fit for this architecture because HeritageGuard requires:

* Structured relational data
* Relationships between assets, inspections and interventions
* Financial/resource constraints
* Geospatial queries
* Optimization inputs

---

## Q8. Why is explainability important?

Conservation decisions can affect culturally significant assets and public resources.

A recommendation must therefore be understandable to the decision-maker.

The system should explain:

```text
Why this asset?
Why this intervention?
Why now?
Why this budget allocation?
```

---

## Q9. Can AI replace conservation experts?

No.

HeritageGuard is designed as a **decision-support system**.

Experts remain responsible for validating:

* Damage interpretation
* Intervention feasibility
* Cultural significance
* Conservation strategy

---

## Q10. What happens if the AI makes a mistake?

The system should use:

* Confidence thresholds
* Human verification
* Expert feedback
* Validation datasets
* Audit trails

AI predictions should not directly trigger irreversible conservation work.

---

## Q11. What if there is not enough real-world data?

The MVP can begin with:

```text
Public computer-vision datasets
+
Small structured prototype asset dataset
+
Expert validation
```

Synthetic data can be used for missing prototype fields, but it must be clearly labelled as synthetic.

---

## Q12. What makes HeritageGuard novel?

The strongest novelty claim is not:

> "We use AI for heritage."

Instead:

> **HeritageGuard integrates visual condition evidence, deterioration, cultural significance, environmental risk, intervention cost and resource constraints into an explainable portfolio-level conservation optimization workflow.**

---

## Q13. What happens if the budget changes?

The optimization model is rerun with the new constraint.

Example:

```text
Budget: ₹20L
       ↓
Portfolio A
```

After budget reduction:

```text
Budget: ₹15L
       ↓
Portfolio B
```

The system explains which interventions changed and why.

---

## Q14. What happens if an intervention is delayed?

The system can update:

```text
Deterioration
Risk
Expected Cost
Preservation Benefit
```

and rerun the optimization.

This allows the authority to compare:

```text
Intervene Now
vs
Intervene Later
```

---

## Q15. What is the biggest technical challenge?

The biggest challenge is not simply training YOLO.

It is obtaining reliable structured information for:

```text
Historical condition
+
Intervention cost
+
Cultural significance
+
Environmental risk
+
Expected preservation benefit
```

because these variables are required by the optimization layer.

---

# 33. Dataset Licensing

Before redistributing any dataset publicly or using it in a commercial product, verify:

* Dataset license
* Redistribution rights
* Attribution requirements
* Commercial-use restrictions
* Original source
* Citation requirements

The fact that a dataset is publicly downloadable does **not** automatically mean that its images can be redistributed freely.

For the HeritageGuard project, dataset sources and citations should be maintained in the documentation.

---

# 34. Team

## HeritageGuard — SIH 2026

**Mentor**

Dr. Chitra A

**Team Leader**

Raj Kamal Bhakat

**Team Members**

* Anas Razy
* Vishnuvikkas J K R
* Manaswee Gadekar
* Suryansh Sinha
* Farazuddin Khan

---

# ⭐ One-Line Project Summary

> **HeritageGuard is an AI-assisted heritage conservation decision-intelligence platform that converts damage evidence and heritage data into explainable, budget-constrained conservation recommendations.**

---

# 🔬 Technical Summary

```text
                    HERITAGEGUARD

             ┌────────────────────────┐
             │   Heritage Data        │
             │ Images + GIS + History │
             └───────────┬────────────┘
                         ↓
             ┌────────────────────────┐
             │ Computer Vision        │
             │ YOLO Damage Detection  │
             └───────────┬────────────┘
                         ↓
             ┌────────────────────────┐
             │ Condition Assessment   │
             └───────────┬────────────┘
                         ↓
             ┌────────────────────────┐
             │ Risk + Deterioration   │
             └───────────┬────────────┘
                         ↓
             ┌────────────────────────┐
             │ Intervention Engine    │
             └───────────┬────────────┘
                         ↓
             ┌────────────────────────┐
             │ OR-Tools Optimization  │
             │ Budget + Resources     │
             └───────────┬────────────┘
                         ↓
             ┌────────────────────────┐
             │ Explainability         │
             │ + What-If Simulation   │
             └───────────┬────────────┘
                         ↓
             ┌────────────────────────┐
             │ Web Dashboard + GIS    │
             └────────────────────────┘
```

---

## Project Philosophy

> **Detect → Understand → Prioritize → Optimize → Explain → Preserve**

HeritageGuard is designed to help conservation authorities make better decisions with limited resources while keeping human experts in the loop.
