# HPDM097_GrpAsg
## Stroke Capacity Planning Simulation (DES Model)

### Table of Contents
1. [Project Overview](#project-overview)
2. [Simulation Model Requirements](#simulation-model-requirements)
3. [Simulation Methodology](#simulation-methodology)
4. [Simulation Parameters](#simulation-parameters)
5. [Patient Transfer Matrix](#patient-transfer-matrix)
6. [Simulation Scenarios](#simulation-scenarios)
7. [Contributors](#contributors)

---

### Project Overview

This project implements a **Discrete-Event Simulation (DES)** to model the **flow of stroke patients** from hospital admission to rehabilitation and early supported discharged (ESD). The simulation helps analyze **capacity bottlenecks, future bed requirements, and the impact of colocation and bed pooling strategies** in a hospital setting. 

The model is based on **46 months of real-world data**, covering **2,444 patient records**, with an **average of 638 admissions per year**.

It is based on the study:

**Monks et al. (2016)** - "A modelling tool for capacity planning in acute and community stroke services"
[Link](https://bmchealthservres.biomedcentral.com/articles/10.1186/s12913-016-1789-4#Tab3)

### Aims & Objectives

The **primary goals** of this simulation are:
- **Identify current capacity bottlenecks** affecting patient flow.
- **Assess future capacity needs** with increased admissions.
- **Evaluate the impact of colocation** and bed pooling between acute and rehabilitation units.
- **Analyze the effect of complex neurological patients** on stroke unit bed demand.

---

### Simulation Model Requirements
#### Patient Breakdown (Admission Categories)
| **Patient Type**                          | **Count**| **Percentage**|
|---|---|---|
| Stroke                                    | 1,320    | 54%           |
| High-risk Transient Ischaemic Attack (TIA)| 158      | 6%            |
| Complex-neurological                      | 456      | 19%           |
| Other                                     | 510      | 21%           |

#### Hospital Bed Capacity
- **Acute Stroke Unit**: 10 beds
- **Community Rehabilitation Unit**: 12 beds

---

### Simulation Methodology
#### Patient Flow Logic
1. **Patient Arrives** -> Admitted to **Acute Stroke Unit** (if beds available).
2. **Treatment in Acute Stroke Unit** (Length of stay follows **log-normal distribution**).
3. **Patient Transfer Decision**:
   - 24% -> Rehabilitation Unit
   - 13% -> Early Supported Discharge (ESD)
   - 63% -> Other (Home, Care Home, Mortality, etc)
4. **Rehabilitation Treatment** (If beds available, LoS follows **log-normal distribution**).
5. **Rehabilitation Discharge**:
   - 40% -> ESD
   - 60% -> Other Destinations
  
#### Modeling Assumptions & Factors Considered
- **Patient type & complexity** (Stroke, TIA, Complex Neurological).
- **Eligibility for ESD** (Some patients move to ESD instead of rehab).
- **Seasonal effects** (Daily/Quarterly variations in demand).
- **Overflow from other hospital wards** (Non-stroke patients using stroke beds).
- **Unfettered Demand Estimation** (Patients floe directly to the required ward if capacity allows).

---

### Simulation Parameters
The following parameters **replicate the base scenario** (current demand levels).

#### Acute Stroke Unit - Length of Stay (LoS)
| **Paatient Type**               | **Mean (days)**| **Std Dev**| **Median**| **5th**| **95th**| **25th**| **75**|
|---|---|---|---|---|---|---|---|
| Strokes (No ESD)                | 7.4            | 8.6        | 4.0       | 1.0    | 23.0    | 2.0     | 9.0   |
| Strokes (ESD)                   | 4.6            | 4.8        | 3.0       | 1.0    | 11.0    | 2.0     | 6.0   |
| Strokes (Mortality)             | 7.0            | 8.7        | 4.0       | 0.5    | 22.0    | 2.0     | 8.0   |
| Transient Ischaemic Attack (TIA)| 1.8            | 2.3        | 1.0       | 0.5    | 4.0     | 1.0     | 2.0   |
| Complex-neurological            | 4.0            | 5.0        | 2.0       | 0.5    | 13.6    | 1.0     | 5.0   |
| Other                           | 3.8            | 5.2        | 2.0       | 0.5    | 12.1    | 1.0     | 5.0   |
- All distribution modeled as log-normal.

#### Rehabilitation Unit - Length of Stay (LoS)
| **Patient Type**                | **Mean (days)**| **Std Dev**| **Median**| **5th**| **95th**| **25th**| **75**|
|---|---|---|---|---|---|---|---|
| Strokes (No ESD)                | 28.4           | 27.2       | 20.0      | 3.0    | 86.9    | 9.0     | 38.0  |
| Strokes (ESD)                   | 30.3           | 23.1       | 22.0      | 6.0    | 78.0    | 13.8    | 44.0  |
| Complex-neurological            | 27.6           | 28.4       | 18.0      | 2.5    | 88.5    | 8.0     | 36.0  |
| Other                           | 16.1           | 14.1       | 11.5      | 1.0    | 43.0    | 5.8     | 24.3  |
| Transient Ischaemic Attack (TIA)| 18.7           | 23.5       | 11.0      | 1.1    | 41.6    | 5.5     | 28.0  |
- All distribution modeled as log-normal.

---

### Patient Transfer Matrix

#### Acute Stroke Unit -> Next Destination
| **Destination** | **Stroke**| **TIA**| **Complex-Neurological**| **Other**|
|---|---|---|---|---|
| Rehabilitation  | 24%       | 1%     | 11%                     | 5%       |
| ESD             | 13%       | 5%     | 5%                      | 10%      |
| Other           | 63%       | 84%    | 84%                     | 85%      |

#### Rehabilitation Unit -> Next Destination
| **Destination**              | **Stroke**| **TIA**| **Complex-Neurological**| **Other**|
|---|---|---|---|---|
| ESD                          | 40%       | 0%     | 9%                      | 13%      |
| Other (Home, Care, Mortality)| 60%       | 100%   | 91%                     | 88%      |

---

### Simulation Scenarios

The model supports different **hospital policy simulations**:
- **Baseline Scenario**: Current acute and rehab bed capacity.
- **Increased Demand**: Simulating a **5% rise in admissions**.
- **Partial Bed Pooling**: Allowing some beds to be shared between acute and rehab patients.
- **Ring-Fencing Beds**: Reserving stroke beds to reduce admission delays.
- **Excluding Complex-Neurological Patients**: Evaluating impact on bed occupancy and patient flow.

---

### Contributors
1. Neil Lenus (nl470@exeter.ac.uk)
2. Emily Sims (es857@exeter.ac.uk)
3. Tan Yi Siew (ut425@exeter.ac.uk)
