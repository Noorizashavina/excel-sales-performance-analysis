# Data Cleaning Log
 
Prepare the sales dataset so revenue, profit, category performance, regional performance, and order quality can be analyzed more accurately.
 
## Data Quality Issues & Resolutions

| Issue Area | What Was Found | Business Risk | Action Taken |
|---|---|---|---|
| Inconsistent categories	| Several entries in the Region, Channel, Status, and Category columns used inconsistent casing and abbreviations. | Inconsistent labels may cause the same category to be treated as separate groups in pivot table or filters. This can distort regional and channel performance analysis. | Trimmed and applied consistent capitalization to the Regional, Channel, Status, and Category columns. Regional abbreviations (JKT, BDG, and SBY) were expanded into full city names (Jakarta, Bandung, and Surabaya). |
| Missing values | The Order Date, Quantity, and Revenue columns contained missing values (null).	| Missing values may understate order volume and revenue totals, leading to inaccurate performance metrics if left unaddressed.	| Flagged rows with missing values in Order Date, Quantity, and Revenue columns for further review, and excluded them from dashboard and summary calculations. |
| Inconsistent date formatting | Order Date values were entered in multiple formats, which are YYYY-MM-DD in Date format, MM/DD/YYYY and DD/MM/YYYY in Text format, and some entries left blank.	| Mixed date formats can cause dates to be misread or fail to convert, distorting monthly trend, and placing orders in the wrong time period.	| Applied a rule-based check. If the first number in the date exceeded 12, the format was read as DD/MM/YYYY. If the second number exceeded 12, it was read as MM/DD/YYYY. Dates where both numbers are 12 or below were treated as ambiguous and set to null. Meanwhile, originally blank dates remained null. |
| Duplicate records |	5 Order IDs appeared more than once in the dataset. |	Duplicate orders may overstate revenue, profit, and order count if it included in analysis without review. |	Used Group By in Power Query to count occurrence of each Order IDs. Rows beyond the first occurrence of a repeated Order ID were flagged as “Duplicate Order” for further review. |
| Numeric fields |	Some values in the Revenue column were stored as text with “Rp” currency symbol. |	Text-formatted numeric values are excluded from calculations, causing revenue and total profits to be understated. |	Converted the Revenue columns to whole numbers with comma thousand separators. |
| Order status |	The dataset included orders marked as Cancelled and Returned. |	Including cancelled or returned orders in performance metrics can overstate actual completed sales.	| Flagged cancelled and returned orders to be analyzed separately from completed orders. |

## Data Quality Summary

| Quality Flag | Rows |
|---|---|
| Clean | 612 |
| Check Quantity | 8 |
| Check Order Date | 18 |
| Check Revenue | 10 |
| Duplicate Order | 5 |
| Review Status | 72 |

*(See the Data Quality Summary sheet in the workbook for the accompanying pie chart.)*
