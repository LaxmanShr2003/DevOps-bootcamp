# Metrics Calculation Report

## **1. Deployment Frequency (per day, assuming 20 working days)**  
**Solution:**  
Total deployment per day = Total deployment / Total working days  
= 40 / 20  
= **2 deployments per day**

---

## **2. Lead Time for Changes**  
**Answer:** The lead time for changes is the time from commit to production which is **3 hours on average**.  
It is usually measured in mean/median.

---

## **3. Change Failure Rate (CFR) (%)**  
**Answer:** The CFR means the percentage of event that cause to deployment failure in production. It requires hot fixes, rollbacks other fixing options.  
As given, there are 6 incidents in total of 40 deployment in a month.

CFR = total incident / total deployment × 100%  
= (6 / 40) × 100%  
= **15%**

Therefore, there was **15% of CRF in total deployment**.

---

## **4. Mean Time to Recovery (MTTR)**  
**Answer:** MTTR means the time to recovey from incident occurred to recovered.

| Incident | Time | Duration |
|---------|--------|-----------|
| Incident 1 | 10:00 → 11:30 | 1.5 hrs = 90 minutes |
| Incident 2 | 14:00 → 14:45 | 0.75 hrs = 45 minutes |
| Incident 3 | 09:00 → 11:00 | 2.0 hrs = 120 minutes |
| Incident 4 | 16:00 → 20:00 | 4.0 hrs = 240 minutes |
| Incident 5 | 13:00 → 13:30 | 0.5 hrs = 30 minutes |
| Incident 6 | 11:00 → 15:00 | 4.0 hrs = 240 minutes |

Now, we need to sum all these time duration = **12.75 hrs**  
MTTR = 12.75 / 6 = **2.125 hours**

This means the total time of **2 hours 7 minutes and 30 seconds** time is taken to recover the incident by the team.

---

## **5. Classification Based on DORA Metrics**  
**Answer:**  

### Comparison to typical DORA ranges:
- **Deployment frequency:**  
  - Elite — multiple times per day  
  - High — once per day to once per week  
  - Medium — once per week to once per month  
  - Low — less than once per month  

- **Lead time for changes:**  
  - Elite — less than 1 day  
  - High — 1 day to 1 week  
  - Medium — 1 week to 1 month  
  - Low — longer  

- **Change failure rate:**  
  - Elite — 0–15%  
  - High — 16–30%  
  - Medium — 31–45%  
  - Low — higher  

- **MTTR:**  
  - Elite — less than 1 hour  
  - High — less than 1 day  
  - Medium — 1 day to 1 week  
  - Low — longer  

### Assessment:
- Deployment frequency (**2/day**) qualifies for **Elite-level frequency**.  
- Lead time (**3 hours**) fits into **Elite / High** velocity thresholds.  
- Change failure rate (**15%**) is the **upper edge of Elite**.  
- MTTR (~**2.13 hours**) is **High performance** (not Elite since Elite is <1 hr).  

### **Final Classification:**  
The team can be categorized as a **High performer**,  
as they don't meet Elite in MTTR making the recovery time duration higher.

---
