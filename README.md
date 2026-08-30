# 🚀 Food Delivery Analytics Challenge

### Turning Delivery Data into Business Decisions

A data-driven analytics project built for the **Food Delivery Analytics Challenge**. This project uses Python and Pandas to analyze **38,964 delivery records**, uncover operational patterns, answer competition questions, and translate the findings into practical business recommendations.

> **Core Principle:** Python performs the analysis. AI explains the results.

---

## 🎯 Project Objective

The goal of this project is to understand the factors affecting food-delivery performance and identify opportunities to:

* Reduce delivery delays
* Improve route efficiency
* Understand the impact of traffic and weather
* Improve delivery reliability
* Support better operational decision-making

**No Machine Learning is required or used.**

---

## 📊 Dataset at a Glance

| Metric           |           Value |
| ---------------- | --------------: |
| Delivery Records |      **38,964** |
| Dataset Type     |   Food Delivery |
| Analysis Tool    | Python + Pandas |
| ML Required      |              No |
| AI Integration   |        Groq LLM |
| Visualizations   |           **3** |

The dataset contains delivery-person information, order timing, location data, weather, traffic, vehicle condition, delivery distance, delivery speed, and delivery time.

---

## 🧹 Data Cleaning & Preparation

Before analysis, the dataset was systematically inspected and cleaned.

### Checks performed

* Missing-value investigation
* Duplicate-record detection
* Numeric data-type validation
* Invalid delivery-time detection
* Invalid distance detection
* Categorical-value handling

Core numerical fields were converted to appropriate numeric types, invalid measurements were handled, and duplicate records were removed before analysis.

This ensured that the competition results were based on clean and reliable data.

---

# 📈 Basic Analysis

The project calculates the following performance indicators programmatically:

* Total deliveries
* Average delivery time
* Minimum delivery time
* Maximum delivery time
* Average delivery distance
* Average delivery speed
* Average delivery-person rating
* Average delivery-person age

### Key Results

| KPI                       |        Result |
| ------------------------- | ------------: |
| Total Deliveries          |    **38,964** |
| Average Delivery Time     | **26.58 min** |
| Average Delivery Distance |   **9.77 km** |
| Average Delivery Rating   |  **4.63 / 5** |

---

# 🏆 Competition Questions

## Q1 — Traffic Impact

**Question:** Which road traffic condition has the highest average delivery time?

The project groups deliveries by `Road_traffic_density` and calculates the average `Time_taken (min)` for each condition.

The result is generated **programmatically**, not hard-coded.

---

## Q2 — Distance Impact

**Question:** How does delivery distance affect delivery time?

The project investigates this relationship using:

* Distance-based grouping
* Average delivery time
* Distance vs delivery-time visualization
* Correlation analysis

This provides both a numerical and visual view of how delivery distance relates to operational time.

---

## Q3 — Combined Conditions

**Question:** Which combination of weather condition and traffic density has the highest average delivery time?

Weather and traffic are grouped together and their average delivery times are calculated.

### Highest-delay condition identified:

**Fog + Jam Traffic → 36.89 minutes**

This is approximately **10 minutes slower** than the overall average delivery time of 26.58 minutes, highlighting a significant operational risk during difficult conditions.

---

# 📊 Visualizations

The project includes three meaningful visualizations.

### 1️⃣ Traffic Density vs Delivery Time

A bar chart comparing the average delivery time across traffic conditions.

**Purpose:** Identify traffic conditions associated with slower deliveries.

### 2️⃣ Delivery Distance vs Delivery Time

A scatter plot showing the relationship between delivery distance and delivery time.

**Purpose:** Understand whether longer delivery distances are associated with longer delivery times.

### 3️⃣ Weather × Traffic Heatmap

A heatmap showing average delivery time for different combinations of weather and traffic conditions.

**Purpose:** Identify high-risk operating conditions.

---

# 💡 Business Insights

## Insight 1 — Delivery Speed

The overall average delivery time is **26.58 minutes**.

**Business meaning:**
Improving dispatching, route planning, and delivery-person assignment can help reduce overall delivery time.

---

## Insight 2 — Route Efficiency

The average delivery distance is **9.77 km**.

**Business meaning:**
Efficient route selection can reduce unnecessary travel, delivery time, fuel consumption, and operating costs.

---

## Insight 3 — Difficult Operating Conditions

The combination of **Fog weather + Jam traffic** produces the highest average delivery time of **36.89 minutes**.

**Business meaning:**
Weather and traffic should be considered together when planning deliveries rather than treating them as completely independent factors.

---

# 🎯 Business Recommendations

### 1. Reduce Delivery Delays

Improve route planning and delivery-person assignment to make dispatching more efficient.

### 2. Optimize Delivery Routes

Use efficient routes to reduce unnecessary travel distance, delivery time, and operating costs.

### 3. Prepare for High-Risk Conditions

When fog and heavy traffic occur, use traffic-aware routing and proactive delivery planning.

### 4. Improve Customer Communication

During high-delay conditions, provide realistic delivery expectations to improve customer experience and service reliability.

---

# 🤖 AI-Powered Explanation

The project integrates the **Groq API** to provide a concise business interpretation of the analytical results.

### Important Architecture

```text
CSV Dataset
     ↓
Python / Pandas
     ↓
Data Cleaning
     ↓
Statistical Analysis
     ↓
Competition Questions
     ↓
Calculated Results
     ↓
Groq LLM
     ↓
Business Explanation
```

### Why this approach?

The LLM does **not** replace the analysis.

Python/Pandas performs:

* Calculations
* Grouping
* Correlation
* Competition-question answers
* Numerical analysis

The LLM receives only the **calculated summary results** and converts them into an understandable business explanation.

This keeps the numerical analysis deterministic and data-driven.

---

# 🔐 API Security

The Groq API key is **not hard-coded** into the project.

The key is accessed through an environment variable:

```text
GROQ_API_KEY
```

Sensitive API credentials should never be uploaded to GitHub.

---

# 🛠️ Technologies Used

| Technology   | Purpose                              |
| ------------ | ------------------------------------ |
| Python       | Core programming                     |
| Pandas       | Data cleaning & analysis             |
| NumPy        | Numerical operations                 |
| Matplotlib   | Visualization support                |
| Seaborn      | Heatmap visualization                |
| Groq API     | AI-powered explanation               |
| Google Colab | Development environment              |
| GitHub       | Version control & project submission |

---

# 📁 Project Structure

```text
food-delivery-analytics/
│
├── food_delivery_dataset.csv
├── Food_Delivery_Analytics.ipynb
│
├── chart1_traffic_vs_time.png
├── chart2_distance_vs_time.png
├── chart3_weather_traffic_heatmap.png
│
└── README.md
```

---

# ▶️ How to Run

### 1. Open the notebook

Open:

```text
Food_Delivery_Analytics.ipynb
```

in Google Colab or Jupyter Notebook.

### 2. Install required libraries

```bash
pip install pandas numpy matplotlib seaborn groq python-dotenv
```

### 3. Configure the Groq API key

Set the API key as an environment variable:

```text
GROQ_API_KEY=your_api_key_here
```

**Never place the actual API key inside the notebook or GitHub repository.**

### 4. Run the notebook

Execute the cells from top to bottom.

---

# 📌 Deliverables

This repository contains:

* ✅ Python analysis notebook
* ✅ Provided CSV dataset
* ✅ Data cleaning
* ✅ Basic statistical analysis
* ✅ Programmatic Q1, Q2 and Q3 answers
* ✅ Two required visualizations
* ✅ Bonus heatmap
* ✅ Three business insights
* ✅ Business recommendations
* ✅ Groq AI-powered explanation
* ✅ Project documentation

---

# 🏁 Conclusion

This project demonstrates how raw food-delivery data can be transformed into actionable business decisions.

The analysis highlights the importance of **delivery speed, route efficiency, traffic conditions, and weather-related risks**.

Rather than simply reporting statistics, the project follows a complete data-analysis workflow:

> **Load → Clean → Analyze → Visualize → Interpret → Explain**

The final objective is simple:

### **Turn Data into Decisions. 📊**
