<p align="center">
  <img src="https://github.com/user-attachments/assets/a58347ae-6a9d-4065-a757-b3d89b92c97d"  width="300"  alt="olistlogo">
</p>

# **Olist Marketplace Retention Analysis**
### **Why 97% of First-Time Buyers Never Return**
## Introduction

### **Who is Olist?**

Olist is a Brazilian e-commerce platform that connects small and medium-sized sellers to large online marketplaces like Mercado Livre. The platform provides tools for order management, logistics integration, payments, and customer support, helping sellers reach customers across Brazil without managing their own infrastructure.

### **The Business Problem**

Between 2016-2018, Olist experienced strong order volume growth (40% YoY) but faced a critical retention crisis: **96.9% of customers made only one purchase and never returned.**   

With rising customer acquisition costs, the growth team was spending heavily to replace churning customers rather than building a loyal buyer base. Leadership needed to understand whether this was fixable through operational improvements or a structural characteristic of their market position.


### **Core Question** 
Are customers leaving because of Olist's operational problems, or is this how Brazilian e-commerce worked in 2016-2018?

**If operational:** Identify the biggest controllable factor (delivery, seller quality, product issues), prove causation, and estimate the value of fixing it.   
**If structural:** Accept that retention will remain low and optimize acquisition efficiency instead.


--------------------


### **Dataset Overview**
**Source:** Brazilian E-Commerce Public Dataset by Olist (**Kaggle**)      
[View Dataset](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce?resource=download)


---------------------------

## **Key Metrics Analyzed:**

- Customer retention and repeat purchase rates
- Delivery performance (on-time vs late)
- Review scores and customer satisfaction
- Seller quality indicators
- Product category mix
- Order values and geographic distribution


# **Executive Summary**
### **The Finding**         
Olist's 97% churn rate is not caused by operational failures. Statistical testing confirmed that even customers with perfect experiences—on-time delivery and 5-star reviews—only returned 3.2% of the time. This is a structural market behavior issue, not a fixable operations problem.

### **Evidence**

- **Delivery performance:** Late delivery (2.57% repeat rate) vs on-time delivery (3.24% repeat rate) shows only 0.67 percentage point difference (χ² = 8.32, p = 0.004)          
- **Customer satisfaction:** Review scores show no relationship with retention—negative reviews (3.10%), neutral (3.18%), and positive (3.18%) all yield identical repeat rates (χ² = 0.23, p = 0.889)       
- **Category variation:** Even naturally repeatable categories (pet supplies, health/beauty) show only 4-5% repeat rates vs 25-40% industry benchmarks       
- **Price and geography:** Order value and customer location show minimal variation in retention (all ~3%)

### **The Root Cause**        
Olist was positioned as a transactional marketplace for one-off purchases, not a relationship platform. Customers used it to find items unavailable locally or to experiment with online shopping, but didn't develop platform loyalty. This was compounded by:

- Early-stage e-commerce trust issues in Brazil (2016-2018)
- Marketplace anonymization (orders appeared under Mercado Livre branding)
- Customer acquisition through price-shopping channels rather than brand building
- Product mix weighted toward durable goods (furniture, appliances) purchased infrequently

### **Business Impact**
Current state vs. marketplace benchmarks:

**Olist repeat rate:** 3.1%      
**Typical marketplace benchmark:** 45-50%        
**Gap:** 42-47 percentage points


At 50,000 new customers per year and $120 average order value, closing even half this gap would represent **$3.6M in additional GMV annually** ($72 incremental value per customer × 50,000 customers).  

However, **operational improvements cannot close this gap** because the problem is structural, not operational.


-------------------------------


# **Analysis & Diagnosis**

### 1. Validating the Retention Crisis

**Finding:** The problem is real and consistent across cohorts.

| Cohort Year | Total Customers | Repeat Customers | Repeat Rate |
|-------------|-----------------|------------------|-------------|
| 2016 | 326 | 13 | 3.99% |
| 2017 | 43,708 | 1,872 | 4.28% |
| 2018 | 52,062 | 1,112 | 2.14% |
| **Overall** | **96,096** | **2,997** | **3.12%** |

Even 2016 customers with 2+ years to repurchase showed only 4% retention. The 2018 decline reflects limited observation time, but the baseline problem existed from the start.

**Customer behavior:** Of the 3% who did return, most made only 2 purchases total. One customer made 17 orders (highest), but 93,099 of 96,096 customers (96.9%) made exactly one purchase.

---

### 2. Testing the Delivery Hypothesis

**Hypothesis:** Late deliveries drive customers away.

**Results:**

| Delivery Performance | Customers | Returned | Repeat Rate |
|---------------------|-----------|----------|-------------|
| Late Delivery | 6,346 | 163 | 2.57% |
| On-Time Delivery | 87,012 | 2,816 | 3.24% |

**Statistical test:** χ² = 8.32, p = 0.004 (statistically significant)

**Business conclusion:** While the relationship is statistically significant, the effect size is operationally meaningless. The 0.67 percentage point difference means that even if Olist eliminated all late deliveries, repeat rate would only increase from 2.57% to 3.24%â€”still a 97% churn rate.

**Implication:** Delivery performance is not the retention driver. Customers with perfect delivery experiences still don't return.

---

### 3. Testing the Customer Satisfaction Hypothesis

**Hypothesis:** Poor experiences (bad reviews) prevent repeat purchases.

**Results:**

| First Order Experience | Customers | Returned | Repeat Rate |
|----------------------|-----------|----------|-------------|
| Negative (1-2 stars) | 11,890 | 368 | 3.10% |
| Neutral (3 stars) | 7,667 | 244 | 3.18% |
| Positive (4-5 stars) | 73,165 | 2,325 | 3.18% |

**Statistical test:** χ² = 0.23, p = 0.889 (not statistically significant)

**Business conclusion:** Review scores have zero relationship with retention. Customers who rated their experience 5 stars are just as unlikely to return as customers who rated it 1 star.

**Implication:** Improving customer satisfaction will not fix retention. The problem runs deeper than service quality.

---

### 4. Testing the Category Mix Hypothesis

**Hypothesis:** The product mix is weighted toward one-time purchase categories.

**Results (Top Categories by Repeat Rate):**

| Category | Customers | Repeat Rate |
|----------|-----------|-------------|
| Home Appliances | 703 | 10.95% |
| Fashion Bags Accessories | 1,798 | 9.12% |
| Furniture Decor | 6,317 | 7.36% |
| Bed Bath Table | 9,145 | 6.58% |
| Sports Leisure | 7,515 | 5.44% |
| **Pet Shop** | **1,689** | **4.97%** |
| **Health Beauty** | **8,678** | **4.16%** |
| **Baby** | **2,858** | **4.16%** |

**Business conclusion:** Category matters, but even "naturally repeatable" categories fail. Pet supplies should have 25%+ repeat rates (pet food is consumable), but Olist shows 4.97%. Health/beauty should be 20-30%, but shows 4.16%.

Home appliances at 11% is the highest category—3.5× the average-likely driven by replacement parts and accessories. But even this "best case" is far below functional retention.

**Implication:** While shifting category mix toward home appliances and fashion accessories would help, it's not sufficient to solve the retention problem. Even best-in-class categories are failing.

---

### 5. Testing Price and Geographic Hypotheses

**Order Value Analysis:**

| Price Bracket | Customers | Repeat Rate |
|--------------|-----------|-------------|
| Under $50 | 18,197 | 3.64% |
| $50-100 | 30,394 | 3.28% |
| $100-200 | 28,842 | 2.98% |
| $200-500 | 12,596 | 3.14% |
| $500+ | 3,329 | 1.95% |

Higher-value customers are actually *less* likely to return. This suggests trust issues with expensive purchases.

**Geographic Analysis (Top States):**

| State | Customers | Repeat Rate |
|-------|-----------|-------------|
| SÃ£o Paulo (SP) | 39,146 | 3.30% |
| Rio de Janeiro (RJ) | 11,912 | 3.53% |
| Minas Gerais (MG) | 10,998 | 3.12% |
| CearÃ¡ (CE) | 1,257 | 1.83% |

Retention is essentially flat across developed (SÃ£o Paulo) and underdeveloped (CearÃ¡) regions. Geographic logistics challenges don't explain the retention crisis.

**Implication:** The problem is platform-wide, not segment-specific. No customer type—regardless of purchase value or location—shows healthy retention.

---

## **Key Insight: Why Operations Don't Matter**

The defining characteristic of this data: **customers with perfect experiences don't come back.**

- On-time delivery + 5-star review → 3.2% repeat rate
- Late delivery + 1-star review → 2.6% repeat rate

A 0.6 percentage point difference between best and worst possible experiences means operational improvements cannot solve retention. The platform was being used for **distress purchases** (items unavailable locally) or **one-time experiments** with online shopping, not as a primary shopping destination.

---

# **Recommendations**

### What Olist Cannot Fix
- **Delivery speed:** Olist is a SaaS platform; sellers control logistics
- **Seller quality at scale:** Removing bad sellers risks losing marketplace breadth
- **Market trust in e-commerce:** Brazil's online shopping adoption was early-stage in 2016-2018

### **Option 1: Stop Fighting Retention—Optimize for Acquisition Efficiency**
**Recommended**

**The strategy:** Accept the 3% baseline and stop wasting budget on retention programs that don't work.

**Actions:**
- Reallocate 60-70% of retention marketing spend (email nurturing, loyalty programs) to acquisition
- Target customer segments expecting one-time purchases: home movers, wedding registries, first-time parents buying nursery furniture
- Partner with life-event platforms (real estate sites, wedding planners) where one-time purchases are natural
- Optimize CAC to break even on first purchase rather than building LTV models

**Business impact:**
- Current retention budget: ~$500k/year → Reallocate $300-350k
- At $20 CAC: +15,000-17,500 new customers
- At $120 AOV: +$1.8-2.1M GMV in Year 1

**Why this works:** Olist controls marketing spend. No logistics or seller changes required.

---

### **Option 2: Shift Category Mix—Build on the 11%**
**Recommended**

**The strategy:** Home appliances show 11% repeat rate (3.5× average). Double down on what works.

**Actions:**
- Recruit 200+ sellers in high-repeat categories (home appliances, fashion accessories, small electronics with consumable parts)
- Analyze what drives home appliance retention (likely: replacement parts, warranty accessories)
- Build category-specific landing pages and marketing campaigns
- De-prioritize furniture and large decor in paid acquisition

**Business impact:**
- Shift 10,000 customers/year from 3% categories to 10% categories
- Current: 300 repeat customers → New: 1,000 repeat customers
- +700 repeat purchases × $120 AOV = +$84k GMV/year
- Compounds in Year 2-3 as the customer base shifts

**Why this works:** Olist controls seller recruitment and marketing focus.

---

### **Option 3: Test a "Second Purchase Guarantee" Program**

**The strategy:** Remove risk from the second purchase to test if trust is the barrier.

**Actions:**
- Offer first-time buyers a one-time guarantee on their second purchase:
  - 30-day return window, no questions asked
  - Free return shipping
  - $10 discount
- Pilot with 10,000 customers in high-repeat categories
- Track redemption rate and third-purchase conversion

**Expected outcomes:**
- 8-12% redemption (vs 3% baseline)
- Cost: $18 per redemption ($10 discount + $8 shipping insurance)
- 10,000 customers × 10% = 1,000 redemptions
- Investment: $18k → Returns: $120k GMV = 5.7 × ROI

**Why test this:** If it fails, you've proven that even eliminating risk doesn't fix trust. If it works, you've found a lever.

---

# **Final Recommendation**

**Implement Option 1 + Option 2 together.**

**Year 1:** Reallocate retention spend to acquisition → +$2M GMV

**Year 2-3:** Category mix shift begins compounding → +$100-250k GMV annually

**3-year impact:** ~$2.5M additional GMV with no changes to logistics, seller contracts, or platform infrastructure.

**Don't implement Option 3 immediately.** The data suggests even perfect experiences don't drive retention, so removing risk likely won't either. Test it only if Options 1 and 2 show that a healthier customer base (acquired through better channels, buying better categories) responds differently.

---

## Methodology Note

This analysis used diagnostic techniques with statistical validation:
- **Chi-square tests** confirmed that delivery and review differences are real but operationally meaningless
- **Cohort analysis** validated that retention problems are consistent across time periods
- **Segmentation analysis** across category, price, and geography isolated the structural nature of the problem

All SQL transformations, hypothesis tests, and data quality checks are available in the project repository.


---

## Key Takeaway

**This project demonstrates diagnostic analysis in a business context:** distinguishing between operational problems (which can be fixed) and structural problems (which require strategic pivots). The retention crisis is real, but throwing resources at delivery speed and customer satisfaction won't solve it. Success requires accepting market reality and optimizing for it, not fighting it.

---

**Author:** Muhammad Aryan  
**Date:** November 2025  
**Tools:** PostgreSQL, Python (scipy), Data Visualization  
**Dataset:** Brazilian E-Commerce Public Dataset by Olist














