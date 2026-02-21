# Marketing Budget Optimization using Linear & Mixed-Integer Programming

##  Executive Summary
This project optimizes the allocation of a $10,000,000 marketing budget across 10 different ad platforms (e.g., Print, TV, SEO, AdWords, Facebook). Using **Gurobi** and Python, we modeled complex, real-world marketing constraints—including diminishing returns, platform spending caps, and minimum investment thresholds—to move budget allocation away from "gut-feel" decisions to mathematically guaranteed optimal returns. 

**[Read the full 10-page Optimization Report here](reports/Group_13_report.pdf)** *(Link assumes you place the PDF in a `reports/` folder)*

## Tech Stack & Tools
* **Optimization Engine:** Gurobi Optimizer (`gurobipy`)
* **Languages & Libraries:** Python, `pandas`, `numpy`
* **Mathematical Modeling:** Linear Programming (LP), Mixed-Integer Programming (MIP), Special Ordered Sets (SOS2)
* **Development Environment:** Jupyter Notebook (EDA), Modular Python Scripts (Production Deployment)

## The Business Problem
Marketing ROI is rarely linear. While initial investments in a platform might yield high returns, those returns eventually diminish (concave). Worse, some platforms require a critical mass of spending before they yield *any* meaningful return, resulting in non-concave, piecewise linear data. 

Standard Linear Programming (LP) fails on non-concave data because it naturally gravitates toward false local optima. This project solves that by implementing a **Mixed-Integer Programming (MIP)** model using Special Ordered Sets of type 2 (SOS2).



## Technical Methodology
The optimization was conducted in two primary phases:

### 1. LP Model (Concave Data)
* Evaluated standard diminishing returns.
* Constraints: Total budget ($10M), maximum platform spend ($3M cap), and categorical spending rules (e.g., Print + TV <= Facebook + Email).

### 2. MIP Model (Non-Concave Data & Advanced Constraints)
* **SOS2 Constraints:** Implemented to handle non-concave piecewise linear ROI, ensuring the model accurately traverses the ROI curve without mathematically "cheating."
* **Minimum Investment Thresholds:** Added binary indicator variables to ensure platforms either received $0 or a strategically meaningful minimum amount (avoiding inefficient micro-investments).
* **Dynamic Reinvestment:** Modeled multi-month allocations where 50% of the previous month's ROI was reinvested into the base budget.
* **Stability Constraints:** Limited month-over-month allocation volatility to ensure the marketing team could practically execute the budget shifts.

## Key Results
* The MIP model successfully navigated the non-linear ROI landscape, diversifying the $10M budget to achieve a mathematically proven maximum return.
* Robustness checks revealed that the $3M individual platform cap was the most binding constraint, heavily dictating the diversification strategy.
* Introducing minimum thresholds significantly refined the allocation, forcing the model to abandon low-impact platforms in favor of dominating higher-yield channels.

