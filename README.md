# Location-Recommendation-System-for-Starbucks-Expansion
Built a Location Scoring System using ML models (XGBoost, Random Forest, Neural Networks) on 20+ datasets (Google Places, US Census, OpenStreetMap) with >10M data rows covering POIs, demographics, city boundaries and Isochrones, to predict store revenue potential and guide strategic expansion identifying both high-revenue and underserved potential locations.

**Project Overview:**

Starbucks, a global coffeehouse leader, operates thousands of locations worldwide. While some stores thrive, others underperform — often due to suboptimal site selection, leading to revenue loss and store closures. This project introduces a scalable, data-driven approach to help Starbucks identify high-potential locations for offline expansion and optimize capital expenditure.

**Problem Statement:**

The Challenge:\
How can Starbucks predict which new store locations are likely to succeed based on demographic, geographic, and competitive data?

The Goal:\
To develop a machine learning pipeline that:

Predicts the likelihood of store success using location-specific features\
Supports smart, data-informed decisions for new store openings

**Data Overview:**

Dataset	Description:

Points of Interest (POIs)	Restaurants, cafes, retail stores, hotels, supermarkets (Google Places API, OSM, Kaggle)\
Demographics	Block-level population, income, age, gender (Census)\
City Boundaries	Geometries of top 20 cities (OpenStreetMap)\
Isochrones	Walking/driving coverage from Starbucks locations (Mapbox)

Data Preparation & Feature Engineering:

1️⃣ Buffer-Based Features\
Created 500m and 1000m buffers around each Starbucks\
Counted POIs by category within each buffer\
Example: number_of_fast_food_restaurants_within_1000m

2️⃣ Isochrone-Based Features\
Generated 5- and 10-minute walking and driving isochrones\
Counted POIs within each time-based reach\
Example: number_of_supermarkets_within_10min_drive

3️⃣ Demographic Features\
Income: % households in income brackets (e.g., $60k–$100k)\
Age: % population by age group\
Gender: Male and female distributions\
Example: pct_households_60_100k

**Pre-Modeling & Feature Selection:**

📊 Kruskal-Wallis Test
Non-parametric test used to check if features significantly differentiate high- vs. low-rated stores.

🌲 Boruta (Tree-Based Models)
Feature selection method that iteratively removes features less important than randomized "shadow features".

🧠 Machine Learning Models

🎯 Classification Task\
Target: Binary label – Store rating above or below 4 stars

Model	Train AUC	Test AUC\
Logistic Regression	0.61	0.68\
XGBoost	0.65	0.64

**Metrics:**

Model	Class	Precision	Recall	F1-score\
Logistic	0	0.63	0.50	0.56\
1	0.68	0.78	0.73\
XGBoost	0	0.59	0.54	0.57\
1	0.68	0.72	0.70

📝 F1-score is crucial here:\
False negatives → Missed opportunity\
False positives → Capital loss on underperforming locations

💡 Key Insights from Feature Impact

Feature	Impact (%)	Insight\
Distance to Nearest Starbucks	-12.02%	- Avoid cannibalizing nearby high-rated stores\
% Households earning $60k–$100k	-9.22% - Strong correlation with better performance\
Presence of Fast Food Restaurants	-8.61%	- Negative impact due to brand dilution\
% Population aged 18–24	-8.41%	- Young adults correlate with higher store ratings\
Supermarkets within 10-min drive	-7.28%	- Attract consistent footfall\
Budget Hotels Nearby	-5.54% -	May negatively affect perception and pricing

**Post-Modeling Analysis:**

🔍 SHAP Feature Importance\
Explains feature impact on individual predictions and global trends

🧭 Recursive Geospatial Clustering (DBSCAN + Haversine)\
Reveals market areas, brand saturation, and expansion gaps\
Helps define micro-clusters of retail activity\
Identifies underrepresented neighborhoods with potential

**Recommendations:**

Open New Stores In:

Locations near existing high-rated Starbucks\
Neighborhoods with $60k–$100k income brackets\
Areas near supermarkets and lightly saturated zones

Avoid:

Fast-food dense areas (negative brand positioning)\
Budget hotel neighborhoods (price-conscious clientele)

**Future Work:**

Direction	- Description

Real-Time Footfall	- Use mobility data to refine traffic estimates\
Sentiment Analysis	- NLP on reviews to uncover quality/location feedback\
Competitor Modeling	- Assess impact of premium/local coffee shops\
Customer Feedback	- Incorporate service ratings and complaint patterns\
Urban Market Dynamics	- Segment cities and adapt strategies per local behavior
