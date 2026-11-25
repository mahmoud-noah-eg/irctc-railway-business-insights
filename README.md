# irctc-railway-business-insights
Power BI dashboard analyzing 20,000 synthetic train bookings

# IRCTC Railway Business Insights (Power BI)

An interactive Power BI dashboard that analyzes 20,000 train bookings made during 2025: bookings, revenue, users, trains, occupancy, routes, booking types and booking channels.

![Dashboard](IRCTC%20business%20dashboard.png)

> **Note:** The data is synthetic and the project is for learning only. It is not affiliated with IRCTC or Indian Railways.

---

## Business questions

1. Which routes drive the network?
2. How much revenue comes from Tatkal bookings?
3. Which booking channels matter most?
4. When is demand highest, and how can the business prepare for it?
5. Are trains full enough to justify adding seats?

---

## Key insights and recommendations

### 1. One route carries a third of the revenue
**Delhi–Mumbai** has 4,403 bookings, which is **22%** of all bookings and **36%** of all revenue.
**Recommendation:** Treat it as the most important route. Monitor delays and cancellations on it closely, and give it priority in maintenance, because a problem here affects over a third of revenue.

### 2. Tatkal brings more revenue per booking
Tatkal (18.12%) and Premium Tatkal (14.65%) together make **32.77% of revenue** from about **27% of bookings**. Their average revenue per booking is higher (roughly ₹2,920 and ₹3,550, against about ₹2,450 for Reserved).
**Recommendation:** Make sure the booking system handles peak load when Tatkal opens, since an outage at that moment loses high-value bookings.

### 3. Digital channels make 88% of revenue
IRCTC Website: ₹28.6M (53.98%). IRCTC App: ₹18.2M (34.29%). Together: **88.27%**. Average revenue per booking is almost the same across channels (about ₹2,570 to ₹2,680), so moving users from the website to the app would shift revenue, not grow it.
**Recommendation:** Keep both channels reliable, and improve the app mainly where it lowers operating cost or improves experience.

### 4. Demand is seasonal
Bookings range from **1,437 in February** to **2,087 in November**, a difference of about 45%. Growth is steady from August to November. December drops about 10.5% from November
**Recommendation:** Prepare systems and capacity for the August to November peak, and run promotions in the weak months (January, February and July) to spread demand across the year. Discounts in November would mostly give away revenue, because demand is already at its highest.

### 5. Occupancy is even, so there is no case for more seats
Average occupancy is **79.92%**, and every train type sits between 79.70% and 80.12%. About 22% of bookings are on trains at 90% occupancy or more, and about 23% are on trains below 70%.
**Recommendation:** Do not add seats to a specific train type. Focus on the emptier trips with offers or schedule changes, and study the full ones in more detail.

---

## Data quality notes

| Issue | What I found | What I did |
|---|---|---|
| Exact duplicate row | 1 row | Removed (19,999 bookings left) |
| Repeated Booking_ID | 349 IDs appear twice with identical details except `Booking_Date` | Kept, and flagged here. Removing them would lower bookings by about 1.7% |
| Travel date before booking date | 59% of rows | Used `Booking_Date` only. `Travel_Date` was not used in the analysis |
| Cancelled, RAC and Waitlisted bookings | About 3.8% of revenue is from cancelled bookings | Included in totals, as the dashboard counts all rows |

---

## A bug worth sharing: month-over-month cards

The first version of the MoM cards showed **+10.31%** for bookings. The correct December vs November change is **-10.49%**.

**Cause:** with no month selected, `DATEADD(..., -1, MONTH)` shifted the full year back one month, so the card compared 20,000 bookings with 18,131 (the same year without December).

**Fix:** show the comparison only when exactly one month is selected.

```dax
Selected Months Count =
DISTINCTCOUNT ( 'Calendar'[Month_Name] )

MoM Booking Growth % =
IF (
    [Selected Months Count] = 1,
    DIVIDE ( [Total Bookings] - [Previous Month Bookings], [Previous Month Bookings] )
)
```

---

## Features

- 5 KPI cards with sparklines and month-over-month change
- Bookings trend with previous-month line and average line
- Revenue by booking type and by booking channel
- Bookings by route
- Slicers: day, month, travel class, train type

---

## Tools

Power BI Desktop, DAX, Excel/CSV cleaning.

---

## Files

```
├── IRCTC.pbix        Power BI report
├── images/           Dashboard screenshots
└── README.md
```

---

## Author

**Mahmoud Noah** 
· LinkedIn: (www.linkedin.com/in/mahmoud-noah) 
. Github: (https://github.com/mahmoud-noah-eg)


