# fintech-fraud-detection

# Intelligent Fraud Shield

##  Project Preview
A high-throughput FinTech data pipeline and machine learning system built for a digital-only bank. The system detects anomalous transactions in milliseconds, resolving extreme class imbalance (0.5% fraud prevalence) to mitigate financial loss while protecting the legitimate user experience.

---

##  Project Title
**Intelligent Fraud Shield: Real-Time Anomaly Detection and Forensic Analytics for NeoPay**

##  Business Problem
Our digital-only bank, **NeoPay**, faces escalating financial losses from Card-Not-Present (CNP) fraud. 
* **The Dilemma:** Overly strict security rules create false positives, blocking honest customers during routine purchases (e.g., a morning coffee) and causing churn. Loose rules create false negatives, leaving the bank to absorb billions in fraudulent losses.
* **The Goal:** NeoPay requires an intelligent system capable of evaluating transaction risk within milliseconds, dynamically balancing security risk against customer convenience.

---

##  Project Objective
To engineer a scalable, end-to-end data and machine learning pipeline that:
1. Identifies and blocks **95% of fraudulent attempts** automatically.
2. Maintains an exceptional customer experience by impacting **less than 0.1% of honest transactions**.
3. Overcomes extreme data asymmetry (class imbalance) where fraudulent transactions make up only 0.5% of total ledger entries.

---

##  Analysis Approach




### 1. SQL (The Forensic Layer)
Engineered rolling behavioral and spatial features directly from raw transaction logs:
* **Spend Deviation:** Calculated `rolling_24h_spend` and `avg_transaction_value` to derive a live `Spend Ratio`.
* **Geographic Velocity:** Evaluated time and distance deltas between consecutive transactions to flag "Geographically Impossible" events (e.g., a card swiped in Lagos, then London 20 minutes later).

### 2. Machine Learning (The Detection Layer)
Built a robust classification pipeline optimized for speed and heavy class imbalance:
* **Resampling:** Deployed **SMOTE** (Synthetic Minority Over-sampling Technique) to address the 0.5% minority class representation.
* **Modeling:** Trained **XGBoost** and **Isolation Forest** algorithms for high-velocity inference.
* **Validation:** Utilized **SHAP (SHapley Additive exPlanations)** beeswarm plots to audit feature importance and eliminate data leakage.

### 3. Tableau (The Surveillance Layer)
Transformed backend model outputs into live operational intelligence:
* Developed **Fraud Heatmaps** to isolate high-risk attack vectors geographically.
* Built an interactive **Threshold Dashboard** allowing executives to simulate financial savings versus customer friction in real-time.

---

##  Visuals
*(Note: Replace placeholder paths with your actual saved image paths or URLs in your repository)*

### 1. The Executive Scatter Plot (Risk Zones)
`![Risk Scatter Plot](path/to/scatter_plot.png)`
* **The Safe Zone (Bottom Left):** A massive, dense cluster representing everyday low-value, local transactions.
* **The Attack Zone (Top Right Cloud):** Highly dispersed anomalous transactions executing at extreme spend ratios and thousands of kilometers away from home.

### 2. Merchant Risk Analysis
`![Merchant Risk Bar Chart](path/to/bar_chart.png)`
* A stark contrast visualization mapping massive transactional volumes against actual fraud counts by category.

### 3. ML Model Explainability (SHAP Beeswarm Plot)
`![SHAP Beeswarm Plot](path/to/shap_plot.png)`
* Shows feature impact on model predictions, highlighting `Amount` as the primary differentiator alongside `Home Region` and `Entry Method` clusters.

---

##  Insights and Recommendations

### Diagnostic Insights
* **The High-Risk Hotspots:** Merchant categories dictate risk. **Electronics, Online Gambling, Jewelry, and Crypto** show a "smoking gun" profile—minimal legitimate transaction volumes but highly concentrated fraud counts. Conversely, Groceries, Dining, and Utilities represent safe, high-volume behavioral baselines.
* **The Driving Signals:** While transaction `Amount` acts as the most aggressive instant flag, relying solely on price risks blocking high-net-worth individuals. Fraud patterns are truly confirmed when a high price tag intersects with a high `Spend Ratio` and anomalous `Entry Method` variables (e.g., manual entry).

### Strategic Recommendations
1. **Automate the High-Risk Filter:** Deploy an immediate transaction block rule for any transaction that exceeds a **5x spend ratio** while concurrently executing in a high-risk category (Electronics/Crypto).
2. **Dynamic Friction Scaling:** Instead of a hard decline for borderline anomalies (the "grey area" transactions), trigger real-time, low-latency SMS or app-based 2-Factor Authentication (2FA) to verify identity without alienating the customer.
3. **Feature Refinement:** Normalize future iterations of the production model by substituting raw transaction amounts with the calculated `Spend Ratio` to safeguard wealthy accounts from false positive flags.
Would you like to build out the exact SQL code block for the "Geographic Jump" calculation next, or should we write the Python code snippet for the XGBoost pipeline?
