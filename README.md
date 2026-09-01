# Food Delivery Analytics & Operational Intelligence

An executive-level operational intelligence platform and interactive dashboard that transforms raw food delivery telemetry into verified statistical findings, interactive visual diagnostics, data-driven business insights, and AI-synthesized strategic briefs.

---

## 1. Project Overview

The **Food Delivery Analytics & Operational Intelligence** system processes thousands of granular last-mile delivery dispatches to identify the root operational causes of fulfillment delays. By replacing guesswork with programmatic statistical analysis, this platform provides dispatchers, fleet operations managers, and executive leadership with dynamic, actionable visibility into how urban congestion, weather conditions, fleet maintenance, and delivery batching impact customer promise times.

---

## 2. Objective

The primary objective of this project is to:
1. **Analyze Delivery Latency**: Identify and quantify the key drivers influencing last-mile order fulfillment cycle times.
2. **Statistically Evaluate External vs. Physical Drivers**: Determine the relative performance penalties induced by road congestion, adverse weather, order batching, and physical travel distance.
3. **Equip Decision-Makers**: Provide interactive data filtering, visual heatmaps, dynamic KPI tracking, exportable audit reports, and AI-assisted operational briefings to improve fleet efficiency and customer satisfaction.

---

## 3. Dataset

The project utilizes the verified food delivery operations dataset:
- **Total Records**: `38,964` completed delivery records.
- **Attributes**: `22` operational and categorical columns.
- **Key Fields**:
  - `ID`, `Delivery_person_ID`: Unique order and driver identifiers.
  - `Delivery_person_Age`: Driver age (numeric).
  - `Delivery_person_Ratings`: Customer satisfaction rating on a 1.0 to 5.0 scale.
  - `Restaurant_latitude`, `Restaurant_longitude`, `Delivery_location_latitude`, `Delivery_location_longitude`: Geospatial pickup and drop-off coordinates.
  - `Order_Date`, `Time_Orderd`, `Time_Order_picked`: Dispatch and pickup timestamps.
  - `Weather_conditions`: Inclement and clear weather categories (*Sunny, Cloudy, Fog, Sandstorms, Stormy, Windy*).
  - `Road_traffic_density`: Operational traffic status (*Low, Medium, High, Jam*).
  - `Vehicle_condition`: Fleet maintenance status (Level 0 = degraded, Level 2 = well-maintained).
  - `Type_of_order`: Order categorization (*Snack, Drinks, Meal, Buffet*).
  - `Type_of_vehicle`: Fleet vehicle classification (*motorcycle, scooter, electric_scooter*).
  - `multiple_deliveries`: Number of stacked orders dispatched per trip (0, 1, 2, 3).
  - `Festival`: Binary/categorical indicator for holiday/festival demand periods.
  - `City`: Urban classification (*Metropolitian, Urban, Semi-Urban*).
  - `distance_km`: Calculated geodesic distance in kilometers between vendor and customer.
  - `Time_taken (min)`: Target operational fulfillment duration in minutes.
  - `delivery_speed`: Categorical speed band classification.

---

## 4. Workflow

```
┌─────────────┐     ┌──────────────┐     ┌──────────────┐     ┌───────────────┐     ┌───────────────┐     ┌───────────────┐
│  Raw Data   │ ──► │ Sanitize &   │ ──► │ Programmatic │ ──► │  Interactive  │ ──► │ Data-Driven   │ ──► │ AI Executive  │
│  Ingestion  │     │ Clean Fields │     │  Statistics  │     │ Visualizations│     │ Action Plan   │     │ Briefing      │
└─────────────┘     └──────────────┘     └──────────────┘     └───────────────┘     └───────────────┘     └───────────────┘
```

1. **Load**: Ingest the raw CSV without mutating the original disk file.
2. **Clean**: Handle whitespace, convert numerical data types, and apply null-safe bounds.
3. **Analyze**: Programmatically calculate correlation matrices, traffic latency deltas, and cross-tabulations.
4. **Visualize**: Generate interactive Plotly dark-themed visualizations (bar charts, scatter plots with OLS trendlines, cross-tab heatmaps).
5. **Interpret**: Translate statistical outputs into direct answers for core operational questions (Q1–Q3).
6. **Explain**: Synthesize quantitative findings into strategic business recommendations and AI executive briefings.

---

## 5. Data Loading & Cleaning

- **Pandas Data Handling**: Data is parsed into memory using Pandas while keeping the underlying CSV immutable.
- **String Sanitization**: Object and string columns are stripped of extraneous whitespace.
- **Type Coercion**: Numerical fields (`Delivery_person_Age`, `Delivery_person_Ratings`, `Time_taken (min)`, `distance_km`, `multiple_deliveries`, `Vehicle_condition`) are cast safely with `errors='coerce'`.
- **Validation**: Programmatic validation checks ensure non-negative distances and positive delivery times.
- **Null-Safety & Accuracy Preservation**: Records with unrecorded partner ages (1,019 rows) or missing feedback ratings (1,055 rows) represent valid completed deliveries and are **not** discarded at initialization.
- **Default Integrity**: Default dashboard sliders and filters maintain **`38,964`** valid orders (100.0% of the dataset) in memory.

---

## 6. Baseline Operational Analysis (Full Dataset)

| Metric | Measured Value | Operational Scope / Details |
| :--- | :--- | :--- |
| **Total Deliveries** | `38,964` | 100.0% of valid dataset |
| **Avg Delivery Time** | `26.6 min` | Median Delivery Time: `26 min` |
| **Avg Distance** | `9.77 km` | Max Distance: `21.0 km` |
| **Dominant Speed** | `Average` | `51.3% of deliveries` |
| **Avg Partner Rating** | `4.63` | Rating Scale: `1.0 - 5.0` |
| **Avg Partner Age** | `29.6 yrs` | Age Range: `20 - 39 yrs` |


---

## 7. Required Questions Answered (Q1 – Q3)

All questions are answered dynamically through real-time Pandas statistical computations rather than hardcoded text:

### Q1: Which traffic condition has the highest average delivery time?
* **Answer**: **Jam** traffic condition causes the highest delivery latency.
* **Evidence**:
  * **Low Traffic**: `~21.3 minutes` average delivery time.
  * **Medium Traffic**: `~26.7 minutes` average delivery time.
  * **High Traffic**: `~27.2 minutes` average delivery time.
  * **Jam Traffic**: `~31.1 minutes` average delivery time.
  * **Operational Drag**: Traffic jams impose an absolute penalty of **`+9.8 minutes per delivery`** (**`+46.0% relative delay`**) compared to free-flowing conditions.

### Q2: How does distance affect delivery time?
* **Answer**: Distance exhibits a positive but **moderate linear correlation** ($r \approx 0.286$, $R^2 \approx 0.082$) with delivery time.
* **Evidence**:
  * Deliveries under **5 km** average **`~22.3 minutes`**.
  * Deliveries between **5–10 km** average **`~26.2 minutes`**.
  * Deliveries between **10–15 km** average **`~26.9 minutes`**.
  * Deliveries over **15 km** average **`~28.5 minutes`**.
  * **Finding**: While longer trips naturally require more travel time, the low $R^2$ demonstrates that non-distance variables (kitchen preparation latency, urban congestion, and severe weather) dominate total fulfillment duration over pure mileage.

### Q3: Which weather + traffic combination has the highest average delivery time?
* **Answer**: Severe atmospheric conditions coupled with congested roads produce the peak latency bottleneck.
* **Evidence**:
  * **Worst Combination**: **Fog / Stormy** weather combined with **Jam** traffic peaks at **`~35.7 minutes`** average delivery duration.
  * **Optimal Combination**: **Sunny** weather combined with **Low** traffic completes fulfillment in **`~14.2 minutes`** on average.
  * **Operational Variance**: A compound swing of **`~21.5 minutes`** (**`~151% variance`**) between best and worst environmental states.

---

## 8. Interactive Visualizations

1. **Road Traffic Density vs. Delivery Time (Bar Chart)**:
   - Illustrates average delivery duration across progressive congestion tiers (*Low → Medium → High → Jam*).
   - Features exact time labels and high-contrast color mapping.
2. **Distance vs. Delivery Time (Scatter Plot + OLS Regression)**:
   - Maps deliveries by mileage and delivery duration with an embedded Ordinary Least Squares (OLS) trendline.
   - Color-coded by traffic density to visually isolate traffic clusters.
3. **Weather Conditions × Traffic Density (Heatmap)**:
   - Two-dimensional matrix displaying average cycle times across every combination of weather and traffic.
   - Highlights high-risk operational bottlenecks for dynamic dispatch adjustments.

---

## 9. Key Business Insights

1. **Traffic Congestion Dominates Physical Distance**:
   Traffic conditions generate an average fulfillment delay increase of **+46.0% (+9.8 min)** between Jam traffic (31.1 min) and Low traffic (21.3 min), establishing traffic density as the primary operational drag.
2. **Fleet Vehicle Health Directly Governs Speed**:
   Vehicles in degraded condition (Level 0, 27.2 min) experience an average penalty of **+3.4 minutes** per delivery run compared to well-maintained vehicles (Level 2, 23.8 min), creating compounding fleet delays across daily runs.
3. **Multi-Drop Order Stacking Friction**:
   Bundling 3 deliveries per trip (30.8 min) increases average per-order latency by **+8.4 minutes** over single-drop dispatches (22.4 min), directly impacting consumer satisfaction.

---

## 10. Strategic Business Recommendations

1. **Dynamic ETA Elasticity & Surge Buffering**:
   - Program real-time dispatch algorithms to automatically expand customer promise windows when traffic sensors register *High* or *Jam*.
   - Deploy surge pricing during concurrent inclement weather and traffic spikes to fund driver overtime incentives.
2. **Intelligent Fleet Allocation & Maintenance Subsidies**:
   - Support regular fleet maintenance for delivery partners to reduce mechanical transit drag.
   - Prioritize high-condition vehicles for higher-density multi-order batches.
3. **Micro-Geofenced Multi-Drop Constraints**:
   - Cap batch sizes to reduced order counts when severe weather (*Fog, Stormy, Sandstorms*) or heavy traffic is detected.
   - Restrict stacking radius during congested windows to preserve food quality and customer satisfaction.
4. **Rider Fatigue & Shift Optimization**:
   - Implement intelligent shift rotation to prevent driver fatigue during sustained peak-hour congestion, preserving service ratings and safety.

---

## 11. AI Executive Strategic Advisor

- **Architecture**: The application leverages Python and Pandas to perform all deterministic mathematical, statistical, and correlation calculations.
- **LLM Context Injection**: Computed metrics (total orders, average time, distance correlation, delay penalties, worst-case weather-traffic pairs) are formatted into an executive prompt and passed to the LLM (Google Gemini / OpenAI).
- **Executive Output**: The AI acts as a Chief Operating Officer, converting numerical results into strategic briefs with identified risk factors and high-ROI interventions.
- **Zero-ML Overhead**: No machine learning regression models or black-box estimators are trained; analytics rely purely on verified descriptive statistics.
- **Security**: API keys are retrieved securely through server-side environment variables and are never displayed or exposed in the UI.

---

## 12. Bonus Features Implemented

* ✅ **Downloadable Filtered Dataset**: Export live filtered data slices directly to CSV with one click.
* ✅ **Downloadable Executive Analysis Summary**: Generate and download formatted `.txt` reports containing metrics, Q1–Q3 statistical answers, and recommendations.
* ✅ **Interactive HTML Chart Downloads**: Download self-contained, interactive Plotly charts as standalone HTML files.
* ✅ **High-Resolution PNG Chart Export**: 1-click 2x scale PNG chart export via embedded Plotly camera controls.
* ✅ **Live Scope Indicator**: Clear display of active subset scope (`Showing X of 38,964 deliveries (Y%)`).
* ✅ **Executive Key Takeaways Banner**: Top-level dashboard component summarizing traffic penalties, distance correlations, and worst-case bottlenecks.
* ✅ **Demo-Friendly "Reset All Filters"**: Instantly restores default parameters (38,964 records) for hackathon evaluators.
* ✅ **Multi-Model Strategic Advisor**: Integrates Gemini and OpenAI LLMs with heuristic offline fallbacks.

---

## 13. Technologies Used

- **Python 3.10+**: Core programming environment.
- **Streamlit**: High-performance interactive dashboard framework.
- **Pandas**: In-memory data manipulation and statistical cross-tabulation.
- **NumPy**: Numerical computation and array operations.
- **Plotly Express & Plotly Graph Objects**: Interactive visual analytics.
- **Statsmodels**: Ordinary Least Squares (OLS) regression for scatter plot trendlines.
- **Python-Dotenv**: Secure environment variable loading.
- **Google Generative AI**: LLM client for executive operational briefing generation.

---

## 14. Project Structure

```
Food_Delivery_Analytics/
├── app.py                             # Main Streamlit dashboard application
├── food_delivery_dataset (1).csv      # Historical delivery telemetry (38,964 rows)
├── requirements.txt                   # Production Python package dependencies
├── .gitignore                         # Git exclusion rules (protects secrets & artifacts)
├── README.md                          # Comprehensive project documentation
├── chart1_traffic_vs_time (2).png     # Exported visualization: Traffic impact
├── chart2_distance_vs_time.png        # Exported visualization: Distance correlation
└── chart3_weather_traffic_heatmap (1).png # Exported visualization: Compound heatmap
```

> **Note**: `.env` is deliberately excluded from version control for security. Users create this file locally to supply their private API key.

---

## 15. Installation & Setup (Windows)

### Step 1: Open Terminal in Project Directory
Open PowerShell or Command Prompt in the project folder:
```powershell
cd C:\Users\Home\Desktop\Food_Delivery_Analytics
```

### Step 2: Install Python Dependencies
```powershell
pip install -r requirements.txt
```

### Step 3: Configure Environment Variables
Create a local `.env` file in the root directory:
```env
GEMINI_API_KEY=your_google_gemini_api_key_here
```
*(Optional: `OPENAI_API_KEY=your_openai_api_key_here`)*

### Step 4: Launch the Streamlit Application
```powershell
streamlit run app.py
```
The interactive dashboard will open automatically in your browser at `http://localhost:8501`.

---

## 16. Security & Credentials Protection

- **No Hardcoded Keys**: API credentials and secrets are strictly loaded via `dotenv` and `os.getenv()`.
- **Git Protection**: `.env` is explicitly registered in `.gitignore` to prevent credential leakage to remote repositories.
- **Client-Side Isolation**: All API queries are handled server-side within Streamlit; no keys are sent to or readable by the browser client.

---

## 17. Hackathon Evaluation Highlights

- **Data Integrity**: Preserves 100% of the 38,964 delivery records upon launch with zero arbitrary data loss.
- **Mathematical Rigor**: Every insight and Q1–Q3 response is backed by real-time statistical aggregations and Pearson correlation calculations.
- **Executive-Grade UI**: Professional glassmorphic dark-theme aesthetics with responsive layout, KPI telemetry, and interactive controls.
- **Practical Business Utility**: Actionable operational interventions directly applicable to enterprise food delivery logistics.
- **Hybrid AI Integration**: Combines deterministic Pandas computation with generative AI synthesis for business strategy.

---

## 18. Conclusion

The **Food Delivery Analytics & Operational Intelligence** platform demonstrates how last-mile logistics operations can shift from reactive troubleshooting to proactive operational planning. By isolating systemic traffic and weather bottlenecks from physical transit distance, delivery networks can optimize dispatch algorithms, safeguard driver safety, and consistently meet consumer expectations.
