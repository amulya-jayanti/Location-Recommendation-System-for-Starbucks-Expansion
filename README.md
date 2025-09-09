# Starbucks Location Recommendation System

This project introduces a data-driven approach to help Starbucks identify high-potential locations for offline expansion. By building a location scoring system with machine learning, we can predict store revenue potential and guide strategic decisions, minimizing capital expenditure on underperforming locations.

---

### **Project Overview**

Starbucks operates thousands of locations, but not all are equally successful. The success or failure of a store is often linked to its location. The goal of this project is to develop a scalable, machine learning-based pipeline that predicts the likelihood of a new store's success based on a wide range of features.

---

### **Methodology**

Our pipeline uses a combination of data preparation, feature engineering, and advanced machine learning models to analyze and score potential locations.

#### **Data and Feature Engineering**

We collected and integrated over 10 million rows of data from more than 20 datasets, including:
* **Points of Interest (POIs):** Restaurants, retail stores, and hotels from sources like Google Places and OpenStreetMap (OSM).
* **Demographics:** Block-level data on population, income, age, and gender from the US Census.
* **Geospatial Data:** City boundaries and travel time (isochrones) from Mapbox and OSM.

We engineered features by:
* Creating **buffer-based features** to count POIs within 500m and 1000m radii.
* Generating **isochrone-based features** to count POIs reachable within 5- and 10-minute walking or driving times.
* Extracting **demographic features** such as the percentage of households in different income brackets.

#### **Feature Selection & Modeling**

To ensure our models were efficient and accurate, we used the **Kruskal-Wallis test** and the **Boruta** algorithm for feature selection.

For the core task of classifying a location as either high-potential (rating > 4 stars) or low-potential, we trained and evaluated several machine learning models. We focused on the **F1-score**, which is critical for balancing the risk of missing a good location (false negative) and opening a failing one (false positive).

| Model | Class (0=Low, 1=High) | Precision | Recall | F1-score |
| :--- | :--- | :--- | :--- | :--- |
| **Logistic Regression** | **0** | **0.63** | **0.50** | **0.56** |
| | **1** | **0.68** | **0.78** | **0.73** |
| **XGBoost** | **0** | **0.59** | **0.54** | **0.57** |
| | **1** | **0.68** | **0.72** | **0.70** |

#### **Key Insights**

We used **SHAP (SHapley Additive exPlanations)** to understand which features had the greatest impact on our model's predictions.

| Feature | Impact (%) | Insight |
| :--- | :--- | :--- |
| **Distance to Nearest Starbucks** | **12.02%** | A strong negative impact, showing the importance of avoiding cannibalization of nearby, high-performing stores. |
| **% Households earning $60k–$100k** | **9.22%** | A strong positive correlation with a store's success. |
| **Presence of Fast Food Restaurants** | **8.61%** | A negative correlation, possibly due to brand dilution. |
| **% Population aged 18–24** | **8.41%** | Young adults correlate positively with higher store ratings. |
| **Supermarkets within 10-min drive**| **7.28%** | Indicates that locations with consistent foot traffic tend to perform better. |

---

### **Recommendations**

Based on our model's insights, we can provide actionable recommendations for strategic expansion:
* **Open Stores In:**
    * Neighborhoods with high-income households ($60k–$100k).
    * Areas near supermarkets that attract consistent footfall.
    * Micro-clusters of retail activity identified through geospatial clustering.
* **Avoid Opening In:**
    * Locations too close to high-performing Starbucks, which can cannibalize sales.
    * Areas dense with fast-food restaurants or budget hotels, as these may signal a brand mismatch.

---

### **Future Work**

Future work will focus on refining the model's accuracy and practicality by:
* Incorporating **real-time mobility data** to get more precise footfall estimates.
* Performing **sentiment analysis** on customer reviews to get a deeper understanding of location-specific feedback.
* Developing **competitor modeling** to assess the impact of other coffee shops.
