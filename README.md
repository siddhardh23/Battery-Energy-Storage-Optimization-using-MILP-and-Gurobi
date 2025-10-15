# ⚡ Battery Energy Storage Optimization using MILP and Gurobi

This project demonstrates how mathematical optimization techniques (MILP) can be applied to **optimize the charging and discharging schedule** of a grid-connected battery system based on hourly electricity market prices. The goal is to **maximize profit** by buying energy when prices are low and selling when prices are high.

---

## 🚀 Project Overview

Energy storage systems are critical for integrating renewable energy into the grid and managing price volatility in electricity markets.  
In this project, we model a battery dispatch problem as a **linear optimization problem** and solve it using **Gurobi** in Python.

**Key highlights:**
- Realistic battery operation modeling with state-of-charge dynamics
- Optimization of charging/discharging schedules based on market prices
- Analysis of system behavior and profitability under different price conditions

---

## 📊 Problem Statement

Given:
- A time series of hourly electricity prices
- Battery characteristics (capacity, charge/discharge power, efficiency, etc.)

We aim to:
- Maximize revenue from charging and discharging
- Subject to physical and operational constraints

---

## 🧮 Optimization Model

**Decision Variables**
- `charge[t]` – energy charged into the battery at hour *t*
- `discharge[t]` – energy discharged from the battery at hour *t*
- `soc[t]` – state of charge of the battery at hour *t*

**Objective Function**
\[
\text{Maximize } \sum_{t=1}^{T} (discharge_t \times price_t - charge_t \times price_t)
\]

**Constraints**
- Energy balance: `soc[t+1] = soc[t] + η × charge[t] - (1/η) × discharge[t]`
- SOC limits: `0 ≤ soc[t] ≤ capacity`
- Power limits: `0 ≤ charge[t] ≤ P_max`, `0 ≤ discharge[t] ≤ P_max`

---

## 🛠️ Tools & Technologies

- **Python** – modeling and data handling  
- **Gurobi** – MILP solver  
- **Pandas** – data manipulation  
- **Matplotlib** – results visualization  

---

## 📁 Project Structure

