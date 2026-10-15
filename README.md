# Customer Segmentation and RFM Analysis

An end-to-end customer analytics project that segments 5,834 customers of an online retailer using RFM (Recency, Frequency, Monetary) analysis, and turns the segments into a suggested marketing budget plan. Built with Python for analysis and Power BI for the dashboard.

---

## Business Problem

Not all customers are equally valuable, and marketing budget is limited. This project answers three questions:

1. Which customers generate most of the revenue?
2. Which valuable customers are at risk of leaving?
3. How should the marketing budget be split across customer groups?

---

## Tools Used

| Area | Tools |
|---|---|
| Data analysis | Python (pandas, numpy) |
| Visualization | matplotlib, seaborn, Power BI |
| Dashboard | Power BI (2 pages, DAX measures,Charts) |

---

## Project Workflow

1. **Data cleaning**
2. **Exploratory data analysis (EDA)**
3. **RFM table creation**
4. **Scoring and segmentation**
5. **Segment analysis and budget recommendation**
6. **Power BI dashboard**

---

## Data Cleaning

- Removed rows with missing `Customer ID` (segmentation needs a customer).
- Removed exact duplicate rows.
- Removed rows with `Price` of zero or less.
- Converted data types (`Customer ID` to integer, `InvoiceDate` to datetime).
- **Handled returns:** returned items are stored as separate negative-quantity rows. Matching purchase and return rows (same customer, product and quantity) were removed together, and unmatched returns were dropped.
- **Removed non-product entries:** postage, manual adjustments, bank charges, discounts and test codes, which are not real purchases.
- Created a `Total_price` column (`Quantity x Price`).

### An outlier that changed the results

EDA showed extreme Quantity values (above 70,000 units in a single order). Checking the raw data showed that these orders were cancelled later by matching negative entries. Removing only the cancellation rows had left the original purchases in the data, which inflated some customers' spending (one customer showed about £77K when the real spend was a few hundred pounds). Matching and removing purchase-return pairs fixed this and changed the final segments.

---

## RFM Analysis

For each customer:

- **Recency:** days since the last purchase (snapshot date = last invoice date + 1 day)
- **Frequency:** number of unique invoices
- **Monetary:** total spend

Each metric was scored from 1 to 5, and customers were assigned to segments with rule-based conditions on the R, F and M scores.

| Segment | Meaning |
|---|---|
| Champions | Bought recently, often, and spend the most |
| Loyal | Regular, good customers |
| Can't Lose | High spenders who have not bought for a long time |
| At-risk | Moderate customers, activity is slowing down |
| Lost | Low value and long inactive |

---

## Key Findings

| Segment | % of Customers | % of Revenue | Avg Spend per Customer |
|---|---|---|---|
| Champions | 17% | 64% | £10,960 |
| At-risk | 44% | 18% | £1,192 |
| Lost | 29% | 3% | £276 |
| Loyal | 7% | 8% | £3,121 |
| Can't Lose | 3% | 6% | £5,313 |

- **Total customers:** 5,834 | **Total revenue:** £16.49M
- Champions are 17% of customers but generate 64% of revenue.
- At-risk and Lost customers make up 73% of customers but only 21% of revenue, so heavy spending on them gives a low return.
- Can't Lose is a small group with a high average spend, which makes it the best win-back target.

---

## Suggested Budget Allocation

| Segment | Budget | Action |
|---|---|---|
| Champions | 50% | Rewards and early access |
| At-risk | 20% | Reminder emails and discounts |
| Can't Lose | 15% | Personal outreach and special offers |
| Loyal | 10% | Keep engaged with loyalty perks |
| Lost | 5% | Low-cost win-back email |

The split is based on each segment's revenue contribution and its potential for recovery. It is a **suggested allocation, not a result derived from the data.**

---

## Power BI Dashboard

**Page 1: Overview**
- KPI cards: Total Customers, Avg Recency, Avg Frequency, Avg Monetary, Total Revenue
- Customers % vs Revenue % by segment
- Average spend per customer by segment
- Segment slicer and key insights

**Page 2: Action Plan**
- Suggested budget allocation
- Recommended action by segment
- Top Can't Lose customers to win back

---


