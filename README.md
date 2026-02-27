# 🚲 Citibike Rebalancing Optimization

Optimizing the pre-peak rebalancing of bike inventory across **689 dock stations** in New York City using integer programming. The project develops progressively realistic optimization models to maximize net revenue by matching bike supply with rider demand during peak commuting hours.

![Python](https://img.shields.io/badge/Python-3.10+-blue?logo=python&logoColor=white)
![Gurobi](https://img.shields.io/badge/Gurobi-Optimization-EE3524)
![Pandas](https://img.shields.io/badge/Pandas-Data_Analysis-150458?logo=pandas&logoColor=white)
![Folium](https://img.shields.io/badge/Folium-Geospatial-77B829)

---

## Problem Context

Citibike is New York's leading bikesharing platform, but approximately **20% of dock stations experience stock-outs during peak hours**, causing lost revenue. A consulting firm estimated that a **4% improvement in operational efficiency** would make the company profitable. This project tackles the core question: *how should bikes be repositioned before the morning rush to maximise revenue?*

---

## Approach

Five optimization models were built with progressively realistic assumptions, all formulated as **integer programs** solved with Gurobi:

| Model | Description | Net Revenue | Gain vs. Baseline |
|-------|------------|-------------|-------------------|
| **Baseline** | No rebalancing | $62,468 | — |
| **Q2: Basic Rebalancing** | Relocate bikes between stations to meet demand | $71,314 | +$8,846 (+14.2%) |
| **Q3: With Replenishment** | Accounts for organic bike returns during peak hour | $75,663 | +$3,639 vs. new baseline |
| **Q4: Vehicle Choice** | Introduces small (SCV, ≤10 bikes, $0.50/km) and large (LCV, $1.00/km) capacity vehicles using Big-M method | $75,882 | Improved via cheaper SCVs |
| **Q5: Procurement Costs** | Adds fixed fees ($80/SCV), per-vehicle costs, and max 3 ops/vehicle | $75,280 | Still profitable under realistic costs |

A **facility location model** (Q6) evaluated opening new stations and found that all 19,050 demand locations already have coverage within 1 km — confirming the bottleneck is **inventory positioning, not network coverage**.

---

## Key Findings

- **Supply-demand mismatch is geographic**: total system inventory (21,169 bikes) exceeds total demand (19,050), but bikes sit at low-demand stations while Midtown and Lower Manhattan face shortages
- **Rebalancing is profitable under all cost assumptions**, delivering $3,600–$8,800 in net revenue gain per peak hour
- **Small vehicles are more cost-effective** for short-distance transfers of ≤10 bikes
- **New stations add zero incremental revenue** — investment should go to demand forecasting and dynamic inventory management instead

---

## Methodology

- **Geospatial analysis** with Folium heatmaps to visualise supply-demand imbalances
- **Integer programming** with Gurobi (decision variables for bike transfers, satisfied demand, vehicle assignments)
- **Big-M formulation** for vehicle type selection constraints
- **Facility location modelling** for network coverage analysis
- **Monte Carlo simulation** of stochastic demand and inventory dynamics (Tutorial 5)

---

## Repository Structure

```
├── Workshop_2_mehmet_eren_celik.ipynb    # Main optimisation models (Q1–Q6)
├── Tutorial_5_Simulation.ipynb           # Stochastic demand simulation extension
├── Executive_Summary_Citibike.pdf        # One-page executive summary
└── README.md
```

---

## Tech Stack

| Component | Technology |
|-----------|-----------|
| Optimisation | Gurobi (gurobipy) |
| Data Processing | pandas, NumPy |
| Visualisation | Folium (heatmaps), Matplotlib, Seaborn |
| Simulation | NumPy (Monte Carlo) |
| Language | Python |

---

## Project Context

Built as part of the **Decision Analytics** course at London Business School (Masters in Analytics & Management, 2025–2026).

---

## Executive Summary

A one-page executive summary with full results and strategic recommendations is included in the repo as `Executive_Summary_Citibike.pdf`.
