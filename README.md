# ⚡ Battery Energy Storage Optimization using MILP and Gurobi

This project demonstrates how to optimize the **charging and discharging schedule** of a grid-connected battery energy storage system (BESS) using **Mixed-Integer Linear Programming (MILP)** and **Gurobi**.  
The goal is to **maximize profit** by charging when electricity prices are low and discharging when prices are high — a core strategy for energy storage systems in modern power markets.

---

## 📊 Project Overview

Energy storage systems are crucial for integrating renewables, balancing supply and demand, and reducing grid volatility.  
This project builds a complete optimization model that:

- Maximizes revenue based on electricity price forecasts.
- Models **state-of-charge dynamics**, **capacity limits**, and **power constraints**.
- Ensures realistic operation using **binary decision variables** (charging and discharging cannot occur simultaneously).
- Outputs a complete operational plan with hourly dispatch, SOC, and total profit.

---

## 🧮 Optimization Problem

### 🎯 Objective Function

The objective is to **maximize revenue** from buying and selling energy:

$$
\max \sum_{t=1}^{T} \left( \text{Discharge}_t \times P_t - \text{Charge}_t \times P_t \right)
$$

Where:
- \( P_t \) = electricity price at hour *t*  
- \( \text{Charge}_t \) = energy charged into the battery (MWh)  
- \( \text{Discharge}_t \) = energy discharged from the battery (MWh)  

---

## ⚙️ Constraints

### 1. **State-of-Charge Dynamics**

The state of charge (SOC) evolves over time based on charging and discharging:

$$
\text{SOC}_{t+1} = \text{SOC}_t + \eta \times \text{Charge}_t - \frac{1}{\eta} \times \text{Discharge}_t
$$

Where:
- \( \eta \) = round-trip efficiency of the battery  
- \( \text{SOC}_t \) = state of charge at time *t*

---

### 2. **SOC Bounds**

The battery SOC must always remain within physical capacity limits:

$$
0 \leq \text{SOC}_t \leq C_{\text{max}}
$$

Where:
- \( C_{\text{max}} \) = battery capacity (MWh)

---

### 3. **Power Constraints**

Charging and discharging power are limited by technical specifications:

$$
0 \leq \text{Charge}_t \leq P_{\text{max}}
$$

$$
0 \leq \text{Discharge}_t \leq P_{\text{max}}
$$

Where:
- \( P_{\text{max}} \) = maximum charge/discharge power (MW)

---

### 4. **Mutual Exclusivity (Binary Condition)**

The battery cannot charge and discharge simultaneously.  
We introduce a binary decision variable \( y_t \):

$$
\text{Charge}_t \leq y_t \times P_{\text{max}}
$$

$$
\text{Discharge}_t \leq (1 - y_t) \times P_{\text{max}}
$$

Where:
- \( y_t = 1 \) → charging mode  
- \( y_t = 0 \) → discharging mode  

---

## 🧰 Technologies Used

- **Python** – Core programming language  
- **Gurobi** – MILP solver  
- **Pandas** – Data handling and analysis  
- **Matplotlib** – Visualization  

---

## 📊 Results

- The optimization schedules charging during **low-price hours** and discharging during **high-price hours**.
- The use of binary variables ensures **realistic operation**.
- The model outputs:
  - Hour-by-hour charging/discharging decisions
  - SOC trajectory over time
  - Total profit from optimized dispatch strategy

Example output:

| Hour | Price (€/MWh) | Charge (MW) | Discharge (MW) | SOC (MWh) |
|------|--------------|--------------|----------------|-----------|
| 0    | 32.5         | 20.0         | 0.0            | 70.0      |
| 1    | 33.2         | 20.0         | 0.0            | 90.0      |
| 2    | 58.7         | 0.0          | 20.0           | 70.0      |

---

## 🧪 Future Improvements

- Add round-trip efficiency and degradation cost modeling  
- Include day-ahead and intraday market participation  
- Extend to multi-battery and multi-site optimization  
- Integrate real-world grid and weather data for forecasting  

---

## 🧠 What I Learned

- Formulating real-world battery dispatch problems as MILP  
- Using **binary decision variables** to model operational constraints  
- Solving optimization problems with Gurobi  
- Translating results into actionable insights for energy trading and storage systems

---

## 👤 Author

**Siddhardha Naidu Gorja**  
M.Sc. Mathematical Modelling, Simulation & Optimization  
Passionate about applying optimization, machine learning, and data science to real-world energy challenges.

---

✅ *“In the world of optimization, every constraint tells a story — and every solution is the art of balancing them.”*

