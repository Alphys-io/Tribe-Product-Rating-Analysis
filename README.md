# 🛍️ Tribe E-Commerce Product Performance Analysis

> Analyzing 26.7M+ product ratings across 1,465 products to uncover actionable insights for e-commerce optimization

## 🎯 Overview

This project provides a comprehensive analysis of product ratings and performance data from **Tribe**, an e-commerce platform. By examining customer sentiment across 9 product categories and 1,465 unique products, the analysis identifies top performers, underperforming segments, and delivers strategic recommendations for inventory optimization and customer satisfaction improvement.

### 📊 Key Metrics at a Glance

| Metric | Value |
|--------|-------|
| **Products Analyzed** | 1,465 |
| **Product Categories** | 9 |
| **Total Customer Ratings** | 26,766,377 |
| **Average Product Rating** | 4.09/5 ⭐ |
| **Data Points Processed** | 1,466 rows × 12 columns |

---

## 🗂️ Dataset

### Source Data Structure

**Initial Dataset:**
- **Rows:** 1,466 (reduced to 1,465 after deduplication)
- **Columns:** 12
- **Content:** Product ratings, reviews, and metadata

### Column Schema

**Original Columns:**
- Product Name
- Category
- Product Rating
- Rating Count
- About Products
- Review Content
- Review ID
- User Name
- Image Link
- Product Link
- User ID

**Derived Columns:**
- Review Remark (Quality classification)
- Rating Tier (Engagement segmentation)

---

## 🧹 Data Cleaning & Transformation

### Step 1: Data Quality Assurance

```excel
✅ Removed 1 duplicate record (1,466 → 1,465 unique products)
✅ Replaced null values in rating count with 1
✅ Standardized category names (removed spacing inconsistencies)
```

### Step 2: Column Optimization

**Removed:** About Products, Review Content, Review ID, User Name  
**Hidden:** Image Link, Product Link, User ID

### Step 3: Feature Engineering

#### 🏷️ Category Extraction
```excel
Extracted first text before delimiter (|) in Category column
Applied Find & Replace to standardize formatting
```

#### 📝 Product Name Standardization
```excel
=TEXTJOIN(" ", TRUE, INDEX(TEXTSPLIT(B2," "), SEQUENCE(3)))
```
- Extracts first 3 words from product names

```excel
=PROPER(SUBSTITUTE(SUBSTITUTE(SUBSTITUTE(SUBSTITUTE(SUBSTITUTE(SUBSTITUTE(SUBSTITUTE(O2,"|",""),"Æ",""),"¬",""),"!",""),"/",""),"(",""),""",""))
```
- Removes special characters and applies proper case

**Example Transformation:**
```
Before: "SYSKA LED Bulb 9W | Cool Day Light | Pack of 4"
After:  "Syska Led Bulb"
```

#### ⭐ Review Remark Classification
```excel
=IF(G2>=5,"Excellent",IF(G2>=4,"Good",IF(G2>=3,"Average",IF(G2>=2,"Poor","Bad"))))
```

| Rating Range | Classification | Icon |
|--------------|----------------|------|
| ≥ 5.0 | Excellent | 🏆 |
| 4.0 - 4.9 | Good | ✅ |
| 3.0 - 3.9 | Average | 🔶 |
| 2.0 - 2.9 | Poor | ⚠️ |
| < 2.0 | Bad | ❌ |

#### 📈 Rating Count Tier
```excel
=IF(AND(I3>=1,I3<=99000),"1 - 99,000",IF(AND(I3>=100000,I3<=199000),"100,000 - 199,000",IF(AND(I3>=200000,I3<=299000),"200,000 - 299,000",IF(AND(I3>=300000,I3<=500000),"300,000 - 400,000+","None"))))
```

| Tier | Range | Segment |
|------|-------|---------|
| **Tier 1** | 1 - 99,000 | Emerging products |
| **Tier 2** | 100,000 - 199,000 | Established products |
| **Tier 3** | 200,000 - 299,000 | Popular products |
| **Tier 4** | 300,000 - 400,000+ | Bestsellers |

#### ✔️ Category Count Validation
```excel
=COUNTA(UNIQUE(Table1[category]))
```
Confirmed **9 unique categories**

---

## 📈 Key Findings

### Review Sentiment Distribution

```
Good Reviews:      23,522,372  ████████████████████████████████████████ 88%
Average Reviews:    3,242,591  █████ 12%
Poor Reviews:           1,386  < 1%
Excellent Reviews:         28  < 1%
```

> **💡 Key Insight:** The overwhelming majority (88%) of reviews are "Good," indicating general customer satisfaction. However, only 28 "Excellent" reviews suggest significant opportunities for improvement in delivering exceptional experiences.

### Category Performance Rankings

#### 🏆 Top Performing Categories (by total ratings)

1. 🖥️ **Electronics** - Highest engagement and rating volume
2. 💻 **Computers & Accessories** - Strong second place
3. 🏠 **Home & Kitchen** - Solid performance

#### 📉 Lower Engagement Categories

- 🎸 Musical Instruments
- 📎 Office Products

### Top-Rated Products

| Product | Rating Count | Avg Rating | Category |
|---------|-------------|------------|----------|
| Syska LED Bulb | 60,000+ | 4.8 | Electronics |
| Amazon Basics HDMI | 50,000+ | 5.0 | Electronics |
| Strepsils Lozenges | 40,000+ | 4.7 | Health & Personal Care |

**Success Pattern:** Established brands + Everyday utility + Competitive pricing + Consistent quality

### Under-Performing Products

| Product | Rating Count | Avg Rating | Issue |
|---------|-------------|------------|-------|
| Boult Bass Headphones | <1,000 | 3.5 | Quality concerns, low visibility |
| Silicone Yoga Mat | <1,000 | 3.2 | Limited reviews, declining trend |

**Common Patterns:** Low review volume, average/below ratings, niche categories, generic/unbranded products

---

## 📊 Dashboard
<img width="6735" height="3255" alt="Dashboard" src="https://github.com/user-attachments/assets/56aa0dd6-f54d-4e65-8f9c-95822a062dbf" />


### Features

- **📌 Key Metrics Cards**: Categories, Products, Average Rating, Total Ratings
- **🎛️ Interactive Filters**: Review Remark Slicer, Rating Tier Slicer, Category Filter
- **📉 Visualizations**: 
  - Category Rating Distribution
  - Review Sentiment Breakdown
  - Top & Under-Performing Products
- **💡 Insights Panels**: Performance Rankings, Product-Level Trends, Quality Distribution



## 💡 Recommendations

### 1. Category Optimization

#### 🎯 Replicate Electronics Success
- Analyze what drives Electronics' high performance (pricing, quality, marketing)
- Apply learnings to under-performing categories
- **Expected Impact:** 15-20% engagement increase

#### 🚀 Revitalize Low-Engagement Categories
- Focus on Musical Instruments and Office Products
- Conduct market research and expand product variety
- Launch targeted marketing campaigns
- **Expected Impact:** 10-15% category growth within 6 months

### 2. Product Portfolio Management

#### 💰 Invest in Winners
- Increase inventory for top performers (Syska, Amazon Basics)
- **Expected ROI:** 25-30% revenue increase

#### 🔧 Address Under-Performers

| Condition | Action |
|-----------|--------|
| Rating < 3.0 & Count < 500 | Consider discontinuation |
| Rating 3.0-3.5 & Count < 1000 | Product improvement plan |
| Rating 3.5-4.0 & Count < 1000 | Marketing boost |

#### ✨ Quality Enhancement Initiative
- Implement stricter supplier QC requirements
- Enhance packaging and after-sales service
- **Target:** Increase "Excellent" ratings from 28 to 10,000+ within 12 months

### 3. Customer Experience Enhancement

#### 🌟 Increase Excellent Reviews
- Implement after-sales service improvements
- Premium packaging for repeat customers
- Personalized thank-you notes and surprise discounts
- **Target:** +5% Excellent ratings

#### 📉 Reduce Average Ratings
- 24-hour response to complaints
- No-questions-asked returns
- Proactive outreach on delayed orders
- **Target:** -50% Average ratings

### 4. Data-Driven Inventory Decisions

**Inventory Allocation Framework:**

| Criteria | Stock Level |
|----------|-------------|
| Rating count ≥ 100,000 & Rating ≥ 4.5 | 90-day stock + buffer |
| Rating count ≥ 50,000 & Rating ≥ 4.0 | 60-day stock |
| Rating count < 500 & Rating < 3.5 | Phase out to clearance levels |

**📊 Monitor monthly trends for all products**

---

## 🛠️ Technical Implementation

### Excel Functions Used

```excel
# Text Processing
TEXTSPLIT()     # Split text by delimiter
TEXTJOIN()      # Join text with separator
INDEX()         # Array indexing
SEQUENCE()      # Generate number sequence
SUBSTITUTE()    # Replace text patterns
PROPER()        # Capitalize text

# Conditional Logic
IF()            # Conditional evaluation
AND()           # Logical AND
NESTED IF()     # Multi-condition evaluation

# Data Analysis
COUNTA()        # Count non-empty cells
UNIQUE()        # Extract unique values
```

### Skills Demonstrated

- ✅ Data Cleaning & Validation
- ✅ Advanced Excel Functions
- ✅ Data Transformation & Feature Engineering
- ✅ Data Visualization & Dashboard Design
- ✅ Statistical Analysis & Business Intelligence
- ✅ Strategic Recommendation Development
- ✅ ROI Analysis & Stakeholder Communication



## 📫 Contact

**Gbenovie Obhoo**  
*Data Analyst*

[![Email](https://img.shields.io/badge/Email-Gbenovieobhoo%40gmail.com-red?style=for-the-badge&logo=gmail)](mailto:Gbenovieobhoo@gmail.com)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?style=for-the-badge&logo=linkedin)](https://linkedin.com/in/gbenovie-obhoo)



## 🙏 Acknowledgments

- Dataset sourced from Tribe E-Commerce platform
- Analysis conducted using Microsoft Excel
- Dashboard design inspired by modern BI best practices

---

<div align="center">

### ⭐ If you found this project helpful, please consider giving it a star!


</div>
