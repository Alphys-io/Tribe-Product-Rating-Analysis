# 🛍️ Tribe E-Commerce Product Performance Analysis

**Analyzing 26.7M+ product ratings across 1,465 products to uncover actionable insights for e-commerce optimization**

## 📊 Project Overview

This project analyzes product ratings and performance data from **Tribe**, an e-commerce platform, examining customer sentiment across 9 product categories and 1,465 unique products. The analysis identifies top performers, underperforming segments, and provides strategic recommendations for inventory optimization and customer satisfaction improvement.

### Key Metrics
- **1,465 products** analyzed across **9 categories**
- **26.7M+ customer ratings** processed
- **4.09/5** average product rating
- Interactive dashboard with filtering capabilities

---

## 🗂️ Dataset Information

**Original Data:**
- 1,466 rows (1,465 after removing duplicates)
- 12 columns
- Product ratings, reviews, and metadata

**Columns Analyzed:**
- Product Name
- Category
- Product Rating
- Rating Count
- Review Remark (Derived)
- Rating Tier (Derived)


## 🧹 Data Cleaning & Preparation

### 1. Data Quality
- ✅ Removed 1 duplicate record (1,466 → 1,465 unique products)
- ✅ Replaced null values in rating count with 1
- ✅ Standardized category names (removed spacing inconsistencies)

### 2. Column Management
**Removed:** About Products, Review Content, Review ID, User Name  
**Hidden:** Image Link, Product Link, User ID

### 3. Data Transformation

#### Category Extraction
excel
Extracted first text before delimiter (|) in Category column

Applied Find & Replace to standardize formatting

Product Name Standardization
=TEXTJOIN(" ", TRUE, INDEX(TEXTSPLIT(B2," "), SEQUENCE(3)))

Extracts first 3 words from product names
=PROPER(SUBSTITUTE(SUBSTITUTE(SUBSTITUTE(SUBSTITUTE(SUBSTITUTE(SUBSTITUTE(SUBSTITUTE(O2,"|",""),"Æ",""),"¬",""),"!",""),"/",""),"(",""),""",""))
Removes special characters and applies proper 
Example:
Before: "SYSKA LED Bulb 9W | Cool Day Light | Pack of 4"
After: "Syska Led Bulb"

Review Remark Classification
=IF(G2>=5,"Excellent",IF(G2>=4,"Good",IF(G2>=3,"Average",IF(G2>=2,"Poor","Bad"))))
Rating Thresholds:
•	🏆 Excellent: ≥ 5.0
•	✅ Good: 4.0 - 4.9
•	🔶 Average: 3.0 - 3.9
•	⚠️ Poor: 2.0 - 2.9
•	❌ Bad: < 2.0
Rating Count Tier
=IF(AND(I3>=1,I3<=99000),"1 - 99,000",IF(AND(I3>=100000,I3<=199000),"100,000 - 199,000",IF(AND(I3>=200000,I3<=299000),"200,000 - 299,000",IF(AND(I3>=300000,I3<=500000),"300,000 - 400,000+","None"))))
Tier Structure:
•	Tier 1: 1 - 99,000 (Emerging products)
•	Tier 2: 100,000 - 199,000 (Established products)
•	Tier 3: 200,000 - 299,000 (Popular products)
•	Tier 4: 300,000 - 400,000+ (Bestsellers)
Category Count Validation
=COUNTA(UNIQUE(Table1[category]))
Confirmed 9 unique categories
________________________________________
###📈 Key Findings
Overall Performance Metrics
Metric	Value
Total Products	1,465
Product Categories	9
Total Ratings	26,766,377
Average Product Rating	4.09/5 ⭐
Review Sentiment Distribution
•	Good Reviews: 23,522,372 (88% of total)
•	Average Reviews: 3,242,591 (12% of total)
•	Poor Reviews: 1,386 (<1%)
•	Excellent Reviews: 28 (<1%)

###Key Insight: The overwhelming majority of reviews are "Good," indicating general customer satisfaction. However, only 28 "Excellent" reviews suggest significant opportunities for improvement in delivering exceptional experiences.
Category Performance Rankings
Top Performing Categories (by total ratings):
1.	🖥️ Electronics - Highest engagement and rating volume
2.	💻 Computers & Accessories - Strong second place
3.	🏠 Home & Kitchen - Solid performance
4.	
**Lower Engagement Categories:**
•	🎸 Musical Instruments
•	📎 Office Products

**Top-Rated Products**
Product	Rating Count	Avg Rating	Category
Syska LED Bulb	60,000+	4.8	Electronics
Amazon Basics HDMI	50,000+	5.0	Electronics
Strepsils Lozenges	40,000+	4.7	Health & Personal Care
Success Pattern: Established brands, everyday utility products, competitive pricing, consistent quality
Under-Performing Products
Product	Rating Count	Avg Rating	Issue
Boult Bass Headphones	<1,000	3.5	Quality concerns, low visibility
Silicone Yoga Mat	<1,000	3.2	Limited reviews, declining trend
Common Patterns: Low review volume, average or below ratings, niche categories, generic/unbranded products
________________________________________
## 📊 Dashboard Preview
 <img width="6735" height="3255" alt="Dashboard" src="https://github.com/user-attachments/assets/c6ad8ab2-7fa8-44ca-935e-d45be030bcff" />

**Dashboard Features**
•	Key Metrics Cards: Categories, Products, Average Rating, Total Ratings
•	Interactive Filters: Review Remark Slicer, Rating Tier Slicer, Category Filter
•	Visualizations: Category Rating Distribution, Review Sentiment Breakdown, Top & Under-Performing Products
•	Insights Panels: Performance Rankings, Product-Level Trends, Quality Distribution
________________________________________
###💡 Strategic Recommendations
1. Category Optimization
**Replicate Electronics Success:**
•	Analyze what drives Electronics' high performance (pricing, quality, marketing)
•	Apply learnings to under-performing categories
•	Expected Impact: 15-20% engagement increase

**Revitalize Low-Engagement Categories:**
•	Focus on Musical Instruments and Office Products
•	Conduct market research and expand product variety
•	Launch targeted marketing campaigns
•	Expected Impact: 10-15% category growth within 6 months

**3. Product Portfolio Management**
Invest in Winners:
•	Increase inventory for top performers (Syska, Amazon Basics)
•	Expected ROI: 25-30% revenue increase

Address Under-Performers:
•	Rating < 3.0 & Count < 500 → Consider discontinuation
•	Rating 3.0-3.5 & Count < 1000 → Product improvement plan
•	Rating 3.5-4.0 & Count < 1000 → Marketing boost

Quality Enhancement Initiative:
•	Implement stricter supplier QC requirements
•	Enhance packaging and after-sales service
•	Target: Increase "Excellent" ratings from 28 to 10,000+ within 12 months

**4. Customer Experience Enhancement**
Increase Excellent Reviews:
•	Implement after-sales service improvements
•	Premium packaging for repeat customers
•	Personalized thank-you notes and surprise discounts
•	Target: +5% Excellent ratings

**Reduce Average Ratings:**
•	24-hour response to complaints
•	No-questions-asked returns
•	Proactive outreach on delayed orders
•	Target: -50% Average ratings

**5. Data-Driven Inventory Decisions**
Inventory Allocation Framework:
•	Rating count ≥ 100,000 & Rating ≥ 4.5 → Maintain 90-day stock + buffer
•	Rating count ≥ 50,000 & Rating ≥ 4.0 → Maintain 60-day stock
•	Rating count < 500 & Rating < 3.5 → Phase out to clearance levels
•	Monitor monthly trends for all products
________________________________________
###🛠️ Technical Skills Demonstrated

•	Data Cleaning & Validation: Removing duplicates, handling null values, standardizing formats
•	Advanced Excel Functions: TEXTSPLIT, TEXTJOIN, INDEX, SEQUENCE, SUBSTITUTE, nested IF statements, COUNTA, UNIQUE
•	Data Transformation & Feature Engineering: Creating derived columns, classification logic
•	Data Visualization & Dashboard Design: Interactive filtering, chart selection, color theory
•	Statistical Analysis & Business Intelligence: KPI development, trend identification, insight generation
•	Strategic Recommendation Development: ROI analysis, stakeholder communication

## 📫 Contact
Gbenovie Obhoo
Data Analyst
📧 Gbenovieobhoo@gmail.com
💼 linkedin/in/gbenovie-obhoo

