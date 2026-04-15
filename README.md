## 📊 AQI Forecasting Project (Chennai)

### 🔍 Model Selection
- Performed exhaustive **AIC grid search** over 9 ARIMAX configurations  
- Selected **`ARIMAX(2,0,1)`** as best model  
  - AIC: **19,204.88** (vs. ~20,355 baseline)  
  - BIC: 19,301.20  
  - Log-Likelihood: −9,585.44  

---

### 📈 Model Performance (Test Set: 80/20 Split)

| Model              | RMSE  | MAE   | Comparison vs Naïve |
|--------------------|------|------|----------------------|
| Naïve (lag-1)      | 19.93 | 13.11 | Baseline             |
| ARIMA(2,0,1)       | 28.47 | 21.45 | ❌ 42.8% worse        |
| **ARIMAX(2,0,1)**  | **18.20** | **12.53** | ✅ **8.7% improvement** |

---

### ⚙️ Feature Engineering
- Engineered **13 exogenous variables**, including:
  - Meteorological factors: `tmin`, `rhum`, `prcp`, `wspd`, `pres`
  - Autoregressive lags: `lag-1`, `lag-7`, `lag-14`
  - Seasonal indicators: **Monsoon phase dummies (4 regimes)**
  - Event indicators: **Diwali window**, **COVID-19 lockdown**
- Ensured low multicollinearity:
  - All **VIF < 3.5**  
- Strong temporal signal:
  - `lag-1` correlation with AQI = **0.75**

---

### ✅ Model Validation
- **ADF Test:** Confirmed stationarity (**p < 0.05**)  
- **Ljung-Box Test (lag 10):**  
  - Q = 15.25, **p = 0.1234**  
  - → Fail to reject white noise (no residual autocorrelation)  
- Residual diagnostics:
  - Approximate **normality** (QQ plot & histogram)

---

### 🧠 Key Takeaways
- Incorporating **exogenous variables significantly improves forecasting accuracy**  
- ARIMAX outperforms both:
  - Naïve baseline  
  - Traditional ARIMA  
- Proper diagnostics confirm **statistical robustness and reliability**

---

### 📌 Notes
- MAPE metric not included (can be added for percentage-based evaluation)  
- Coefficient-level statistical significance available via SARIMAX summary output  
