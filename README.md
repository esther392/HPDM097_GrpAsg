# HPDM097_GrpAsg
## Stroke Capacity Planning Simulation

### Table of Contents
1. [Project Overview](#project-overview)
2. [Simulation](#simulation)
3. [Model Assumptions](#model-assumptions)
4. [Contributors](#contributors)

---

### Project Overview

This project implements a **Discrete-Event Simulation (DES)** model for capacity planning in acute and community stroke services. It is based on the study:

**Monks et al. (2016)** - "A modelling tool for capacity planning in acute and community stroke services"
[Link](https://bmchealthservres.biomedcentral.com/articles/10.1186/s12913-016-1789-4#Tab3)

The simulation models patient flow through an acute stroke unit, community rehabilitation, and early supported discharged (ESD). The goal is to assess **bed allocation**, **patient delays**, and **the impact of different capacity planning strategies** using **SimPy** in **Python**.

---

### Simulation

This project evaluates different **capacity planning strategies**:
- **Baseline Scenario**: Current acute and rehab bed capacity.
- **Increased Demand**: Simulating a **5% rise in admissions**.
- **Partial Bed Pooling**: Allowing some beds to be shared between acute and rehab patients.
- **Ring-Fencing Beds**: Reserving stroke beds to reduce admission delays.
- **Excluding Complex-Neurological Patients**: Evaluating impact on bed occupancy and patient flow.

---

### Model Assumptions

- **Patient Arrivals**: Follow an **exponential distribution**.
- **Length of Stay (LoS)**: Modeled using a **log-normal distribution**:
  
| **Parameters**       | **Mean (days)**| **Std Dev (days)**|
|---|---|---|
| Strokes (No ESD)     | 7.4            | 8.6               |
| Strokes (ESD)        | 4.6            | 4.8               |
| Strokes (Mortality)  | 7.0            | 8.7               |
| TIA                  | 1.8            | 2.3               |
| Complex-neurological | 4.0            | 5.0               |
| Other                | 3.8            | 5.2               |

- **Bed Occupancy**: Follow an **poisson distribution**.
- **Bed Allocation logic**:
  - Patients enter **acute stroke unit** first.
  - Then transfer to **rehab, ESD, or other destinations** based on probabilities.
  - **Queueing rules apply** when no beds are available.

---

### Contributors
1. Neil Lenus (nl470@exeter.ac.uk)
2. Emily Sims (es857@exeter.ac.uk)
3. Tan Yi Siew (ut425@exeter.ac.uk)
