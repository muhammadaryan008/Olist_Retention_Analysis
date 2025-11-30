### First Step: Validate the Core Problem
- Before diagnose anything, confirm the retention problem is real and worth solving.
```sql
-- Cohort analysis by first purchase year
SELECT 
    EXTRACT(YEAR FROM cohort_month) as cohort_year,
    COUNT(DISTINCT customer_unique_id) as total_customers,
    COUNT(DISTINCT CASE WHEN is_repeat_customer = 1 THEN customer_unique_id END) as repeat_customers,
    ROUND(100.0 * COUNT(DISTINCT CASE WHEN is_repeat_customer = 1 THEN customer_unique_id END) / 
          COUNT(DISTINCT customer_unique_id), 2) as repeat_rate_pct
FROM summary
GROUP BY EXTRACT(YEAR FROM cohort_month)
ORDER BY cohort_year;
```
Here is the output of the query:

- **93,102** out of **96,099** customers **(96.9%)** made exactly one purchase. That's the core problem.
- **3.1% repeat rate.**

<img width="550" height="150" alt="Screenshot 2025-11-29 at 3 59 35 PM" src="https://github.com/user-attachments/assets/91c17497-d8d7-4d2c-b22e-fd0b1ddf05db" />

### Step 2: Test the Delivery Hypothesis
- The brief assumes delivery performance is the main driver.
```sql
-- Compare late delivery rates between one-time vs repeat customers
SELECT 
    CASE WHEN is_repeat_customer = 1 THEN 'Repeat Customer' ELSE 'One-Time Customer' END as customer_type,
    COUNT(*) as total_orders,
    SUM(CASE WHEN is_late = 1 THEN 1 ELSE 0 END) as late_orders,
    ROUND(100.0 * SUM(CASE WHEN is_late = 1 THEN 1 ELSE 0 END) / COUNT(*), 2) as late_rate_pct,
    ROUND(AVG(delivery_time_days), 2) as avg_delivery_days,
    ROUND(AVG(shipping_delay), 2) as avg_delay_days
FROM summary
WHERE order_status = 'delivered'
GROUP BY CASE WHEN is_repeat_customer = 1 THEN 'Repeat Customer' ELSE 'One-Time Customer' END;
```
Here is the output of the query:

<img width="641" height="500" alt="Screenshot 2025-11-30 at 11 36 19 AM" src="https://github.com/user-attachments/assets/95476a07-9cf4-435a-acae-2465532bbc11" />



```sql
-- For first-time orders only, does late delivery predict whether they return?
SELECT 
    CASE WHEN is_late = 1 THEN 'Late Delivery' ELSE 'On-Time Delivery' END as delivery_performance,
    COUNT(DISTINCT customer_unique_id) as customers,
    COUNT(DISTINCT CASE WHEN is_repeat_customer = 1 THEN customer_unique_id END) as customers_who_returned,
    ROUND(100.0 * COUNT(DISTINCT CASE WHEN is_repeat_customer = 1 THEN customer_unique_id END) / 
          COUNT(DISTINCT customer_unique_id), 2) as return_rate_pct
FROM (
    SELECT DISTINCT ON (customer_unique_id)
        customer_unique_id,
        is_late,
        is_repeat_customer,
        order_purchase_timestamp
    FROM summary
    WHERE order_status = 'delivered'
    ORDER BY customer_unique_id, order_purchase_timestamp
) first_orders
GROUP BY CASE WHEN is_late = 1 THEN 'Late Delivery' ELSE 'On-Time Delivery' END;
```
Here is the output of the query:

<img width="517" height="94" alt="Screenshot 2025-11-30 at 11 47 39 AM" src="https://github.com/user-attachments/assets/c5260957-918e-4cd8-b191-b5b9f1a22039" />



```sql
-- Does review score on first order predict return?
SELECT 
    CASE 
        WHEN review_score >= 4 THEN 'Positive (4-5 stars)'
        WHEN review_score = 3 THEN 'Neutral (3 stars)'
        ELSE 'Negative (1-2 stars)'
    END as review_category,
    COUNT(DISTINCT customer_unique_id) as customers,
    COUNT(DISTINCT CASE WHEN is_repeat_customer = 1 THEN customer_unique_id END) as customers_who_returned,
    ROUND(100.0 * COUNT(DISTINCT CASE WHEN is_repeat_customer = 1 THEN customer_unique_id END) / 
          COUNT(DISTINCT customer_unique_id), 2) as return_rate_pct
FROM (
    SELECT DISTINCT ON (customer_unique_id)
        customer_unique_id,
        review_score,
        is_repeat_customer,
        order_purchase_timestamp
    FROM summary
    WHERE order_status = 'delivered' AND review_score IS NOT NULL
    ORDER BY customer_unique_id, order_purchase_timestamp
) first_orders
GROUP BY CASE 
    WHEN review_score >= 4 THEN 'Positive (4-5 stars)'
    WHEN review_score = 3 THEN 'Neutral (3 stars)'
    ELSE 'Negative (1-2 stars)'
END;
```
Here is the output of the query:

<img width="489" height="121" alt="Screenshot 2025-11-30 at 11 50 11 AM" src="https://github.com/user-attachments/assets/f66f5508-aed9-4c96-af40-0c36d02df66b" />












