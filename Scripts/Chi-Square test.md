## **Statistical Test: Chi-Square Analysis**
**SQL Query - Extract Contingency Table:**
```sql
-- Export this data for chi-square test
SELECT 
    CASE WHEN is_late = 1 THEN 'Late' ELSE 'OnTime' END as delivery_status,
    CASE WHEN is_repeat_customer = 1 THEN 'Repeat' ELSE 'OneTime' END as customer_type,
    COUNT(DISTINCT customer_unique_id) as count
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
GROUP BY 
    CASE WHEN is_late = 1 THEN 'Late' ELSE 'OnTime' END,
    CASE WHEN is_repeat_customer = 1 THEN 'Repeat' ELSE 'OneTime' END;
```
**Query Results:**

<img width="308" height="140" alt="Screenshot 2025-11-30 at 4 48 25 PM" src="https://github.com/user-attachments/assets/38f6dc88-f914-453f-bad3-a0bc66ba7cd4" />


**Python - Chi-Square Test:**
```python
from scipy.stats import chi2_contingency

observed = [[163, 6183], [2816, 84196]]
chi2, p_value, dof, expected = chi2_contingency(observed)

print(f"Chi-square statistic: {chi2}")
print(f"P-value: {p_value}")
print(f"Conclusion: {'Significant' if p_value < 0.05 else 'Not significant'}")
```
**Test Results:**

<img width="434" height="116" alt="Screenshot 2025-11-30 at 4 50 30 PM" src="https://github.com/user-attachments/assets/a91acda2-6d04-4efa-97c7-55765cf4e114" />


## **Statistical Result:**

Chi-square = 8.32, p-value = 0.0039 (< 0.05)
Conclusion: The difference IS statistically significant
Translation: "Late delivery and repeat purchases are related - this isn't random chance"

**Business Reality:**

Late delivery: 2.57% repeat rate (163 out of 6,346)
On-time delivery: 3.24% repeat rate (2,816 out of 87,012)
Difference: 0.67 percentage points

**The Key Insight:**
Yes, late delivery statistically reduces repeat purchases. But the effect is so small it doesn't matter operationally.



