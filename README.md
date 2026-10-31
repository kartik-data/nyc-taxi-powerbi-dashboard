# NYC Yellow Taxi Earnings Analysis (January 2026) | Power BI

A Power BI dashboard built on 3.5 million real NYC yellow taxi trips, answering one question: **when and where do taxis earn the most?**







## Business Question

A taxi fleet manager wants to increase earnings. Using January 2026 trip data, which zones, days and hours generate the most revenue, and what should the fleet do about it?

## Data Source

* **NYC Taxi \& Limousine Commission (TLC) Trip Record Data**, Yellow Taxi, January 2026 (Parquet)
* **Taxi Zone Lookup Table** (CSV) from the same source
* Public open data. No personal information (no passenger names or driver IDs).
* Raw data is not included in this repository. Download it from the NYC TLC website.

## Tools

Power BI Desktop (Power Query, data modeling, DAX, visuals)

## Process

### 1\. Clean and transform (Power Query)

* Kept only the columns needed for the analysis
* Set correct data types
* Created helper columns: trip minutes, pickup hour, pickup date, weekday
* Removed invalid records:

  * Pickup dates outside January 2026
  * Zero or negative distance, and unrealistic distances
  * Zero, negative or unrealistic trip duration
  * Zero or negative fare and total amount
  * Dropoff time earlier than pickup time
* Rows after cleaning: **3,519,048**





### 2\. Data model (star schema)

* `Trips` (fact table)
* `Dim\_Date` (date table, related on pickup date)
* `Zones` (lookup table, related on pickup location ID)
* `Payment type` lookup table (codes mapped to names)

### 3\. DAX measures

* Total Trips, Total Revenue, Average Daily Revenue, Average Daily Trips
* Revenue per Minute (revenue divided by trip minutes)
* Total Tip Amount
* Average revenue per trip

### 4\. Dashboard

KPI cards, daily revenue trend, average revenue by weekday, trips by pickup hour, revenue by payment type, top pickup zones, and borough and weekday filters.

## Key Findings

|Metric|Value|
|-|-|
|Total trips|3.52M|
|Total revenue|$102.25M|
|Average daily revenue|$3.30M|
|Average revenue per trip|$29.06|
|Revenue per minute|$1.69|

1. **Airports earn much more per trip.** JFK (146K trips, $73.11 per trip) and LaGuardia (82K trips, $66.47 per trip) are about 6.5% of trips but about 16% of revenue.
2. **Volume is not the same as value.** Upper East Side South has the most trips among the top zones (152K) but only $21.30 per trip.
3. **The week has a clear pattern.** Tuesday to Saturday earn about $3.4M to $3.7M per day, while Sunday ($2.5M) and Monday ($2.6M) earn roughly 30% less.
4. **Cards dominate payments.** Credit card is about 63% of revenue, Flex Fare about 30% and cash about 7%.
5. **One unusual day.** January 25 was the lowest day at about $1.3M. I have not verified the cause, so I treat it as an open question.



## Limitations

* Revenue uses the `total\_amount` field, which includes tips, taxes, tolls and fees. It is not the driver's income.
* The data has no driver ID or idle time, so Revenue per Minute counts only time with a passenger.
* Tips are recorded only for card payments.
* The analysis covers one month. Seasonal conclusions need more months.
* Cleaning thresholds are my own judgment, not official TLC rules.



## About Me

IT student looking for a 3-6 month data analyst internship in Mumbai, available immediately.

