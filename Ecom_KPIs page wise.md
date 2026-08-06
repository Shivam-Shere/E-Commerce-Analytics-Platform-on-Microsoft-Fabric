KPIs  





\## Last Refresh Date: (e.g., Last Refresh: 02 Aug 2026 02:52 PM)



1\. Last Refresh = "Last Refresh: " \& FORMAT(NOW(), "dd MMM yyyy hh:mm AM/PM")



2\. Last Refresh = 

VAR RefreshTime = FORMAT(NOW(), "dd MMM yyyy hh:mm AM/PM")

RETURN

"Last Refreshed"

&#x20;   \& UNICHAR(10)

&#x20;   \& RefreshTime











# Page-1. Overview Analysis: 





{Total Orders/ Total Customers/ Total Revenue (Sales)/ Total Products Sold (Products)/ Total Sellers (Dealers)/ AVG Review Rating/ Total Payment Value}  



{AVG Order Value/ On Time Delivery Rate}





1\. Total Orders:



a. Total Orders= DISTINCTCOUNT(fact\_orders\[order\_id])



b. Total Orders % =

DIVIDE(

&#x20;   \[Total Orders],

&#x20;   CALCULATE(\[Total Orders], ALL(dim\_date)),

&#x20;   0

)



c. PY Total Orders =

CALCULATE(

&#x20;   \[Total Orders],

&#x20;   SAMEPERIODLASTYEAR(dim\_date\[date])

)



d. YoY Total Orders =

IF(

&#x20;   ISBLANK(\[PY Total Orders]),

&#x20;   BLANK(),

&#x20;   \[Total Orders] - \[PY Total Orders]

)



e. YoY % Total Orders =

VAR PrevYear =

COALESCE(\[PY Total Orders],0)



RETURN

IF(

&#x20;   PrevYear=0,

&#x20;   0,

&#x20;   DIVIDE(\[YoY Total Orders],PrevYear,0)

)







2\. Total Customers:



a. Total Customers = DISTINCTCOUNT(fact\_orders\[customer\_id])



b. Total Customers % =

DIVIDE(

&#x20;   \[Total Customers],

&#x20;   CALCULATE(\[Total Customers],ALL(dim\_date)),

&#x20;   0

)



c. PY Total Customers =

CALCULATE(

&#x20;   \[Total Customers],

&#x20;   SAMEPERIODLASTYEAR(dim\_date\[date])

)



d. YoY Total Customers =

IF(

ISBLANK(\[PY Total Customers]),

BLANK(),

\[Total Customers]-\[PY Total Customers]

)



e. YoY % Total Customers =

VAR PrevYear =

COALESCE(\[PY Total Customers],0)



RETURN



IF(

PrevYear=0,

0,

DIVIDE(\[YoY Total Customers],PrevYear,0)

)







3\. Revenue:



a. Total Revenue = SUM(fact\_order\_payment\[payment\_value])



b. Revenue % =

DIVIDE(

\[Total Revenue],

CALCULATE(\[Total Revenue],ALL(dim\_date)),

0

)



c. PY Revenue =

CALCULATE(

\[Total Revenue],

SAMEPERIODLASTYEAR(dim\_date\[date])

)



d. YoY Revenue =

IF(

ISBLANK(\[PY Revenue]),

BLANK(),

\[Total Revenue]-\[PY Revenue]

)



e. YoY % Revenue =

VAR PrevYear=

COALESCE(\[PY Revenue],0)



RETURN



IF(

PrevYear=0,

0,

DIVIDE(\[YoY Revenue],PrevYear,0)

)







4\. Total Products Sold:



a. Products Sold = COUNTROWS(fact\_order\_items)



b. Products Sold % =

DIVIDE(

\[Products Sold],

CALCULATE(\[Products Sold],ALL(dim\_date)),

0

)



c. PY Products Sold =

CALCULATE(

\[Products Sold],

SAMEPERIODLASTYEAR(dim\_date\[date])

)



d. YoY Products Sold =

IF(

ISBLANK(\[PY Products Sold]),

BLANK(),

\[Products Sold]-\[PY Products Sold]

)



e. YoY % Products Sold =

VAR PrevYear=

COALESCE(\[PY Products Sold],0)



RETURN



IF(

PrevYear=0,

0,

DIVIDE(\[YoY Products Sold],PrevYear,0)

)







5\. Total Sellers:



a. Total Sellers = DISTINCTCOUNT(fact\_order\_items\[seller\_id])



b. Total Sellers % =

DIVIDE(

&#x20;   \[Total Sellers],

&#x20;   CALCULATE(

&#x20;       \[Total Sellers],

&#x20;       ALL(dim\_date)

&#x20;   ),

&#x20;   0

)



c. PY Total Sellers =

CALCULATE(

&#x20;   \[Total Sellers],

&#x20;   SAMEPERIODLASTYEAR(dim\_date\[date])

)



d. YoY Total Sellers =

IF(

&#x20;   ISBLANK(\[PY Total Sellers]),

&#x20;   BLANK(),

&#x20;   \[Total Sellers] - \[PY Total Sellers]

)



e. YoY % Total Sellers =

VAR PrevYear =

&#x20;   COALESCE(\[PY Total Sellers], 0)



RETURN

IF(

&#x20;   PrevYear = 0,

&#x20;   0,

&#x20;   DIVIDE(

&#x20;       \[YoY Total Sellers],

&#x20;       PrevYear,

&#x20;       0

&#x20;   )

)







6\. AVG Review Rating:



a. Avg Review Rating = AVERAGE(fact\_order\_reviews\[review\_score])



b. Avg Review Rating % =

DIVIDE(

&#x20;   \[Avg Review Rating],

&#x20;   CALCULATE(

&#x20;       \[Avg Review Rating],

&#x20;       ALL(dim\_date)

&#x20;   ),

&#x20;   0

)



c. PY Avg Review Rating =

CALCULATE(

&#x20;   \[Avg Review Rating],

&#x20;   SAMEPERIODLASTYEAR(dim\_date\[date])

)



d. YoY Avg Review Rating =

IF(

&#x20;   ISBLANK(\[PY Avg Review Rating]),

&#x20;   BLANK(),

&#x20;   \[Avg Review Rating] - \[PY Avg Review Rating]

)



e. YoY % Avg Review Rating =

VAR PrevYear =

&#x20;   COALESCE(\[PY Avg Review Rating], 0)



RETURN

IF(

&#x20;   PrevYear = 0,

&#x20;   0,

&#x20;   DIVIDE(

&#x20;       \[YoY Avg Review Rating],

&#x20;       PrevYear,

&#x20;       0

&#x20;   )

)





7\. Total Payment Value:



a. Total Payment Value = SUM(fact\_order\_payments\[payment\_value])



b. Total Payment Value % =

DIVIDE(

&#x20;   \[Total Payment Value],

&#x20;   CALCULATE(

&#x20;       \[Total Payment Value],

&#x20;       ALL(dim\_date)

&#x20;   ),

&#x20;   0

)



c. PY Total Payment Value =

CALCULATE(

&#x20;   \[Total Payment Value],

&#x20;   SAMEPERIODLASTYEAR(dim\_date\[date])

)



d. YoY Total Payment Value =

IF(

&#x20;   ISBLANK(\[PY Total Payment Value]),

&#x20;   BLANK(),

&#x20;   \[Total Payment Value] - \[PY Total Payment Value]

)



e. YoY % Total Payment Value =

VAR PrevYear =

&#x20;   COALESCE(\[PY Total Payment Value], 0)



RETURN

IF(

&#x20;   PrevYear = 0,

&#x20;   0,

&#x20;   DIVIDE(

&#x20;       \[YoY Total Payment Value],

&#x20;       PrevYear,

&#x20;       0

&#x20;   )

)







# Page-2. Sales Analysis:



Kpis= {Total Freight Cost/ Average Order Value (AOV)/ Average Selling Price (ASP)/ Revenue  per Product} 



{Revenue per Seller/ Revenue per Customer}





1\. Revenue per Product:  (Total Revenue ÷ Total Products Sold)



a. Revenue per Product =

DIVIDE(

&#x20;   \[Total Revenue],

&#x20;   DISTINCTCOUNT(fact\_order\_items\[product\_id]),

&#x20;   0

)





OR



Revenue per Product =

DIVIDE(

&#x20;   \[Total Revenue],

&#x20;   \[Total Products],

&#x20;   0

)





b. Revenue per Product % =

DIVIDE(

&#x20;   \[Revenue per Product],

&#x20;   CALCULATE(

&#x20;       \[Revenue per Product],

&#x20;       ALL(dim\_date)

&#x20;   ),

&#x20;   0

)





c. PY Revenue per Product =

CALCULATE(

&#x20;   \[Revenue per Product],

&#x20;   SAMEPERIODLASTYEAR(dim\_date\[date])

)





d. YoY Revenue per Product =

IF(

&#x20;   ISBLANK(\[PY Revenue per Product]),

&#x20;   BLANK(),

&#x20;   \[Revenue per Product] - \[PY Revenue per Product]

)



e. YoY % Revenue per Product =

VAR PrevYear =

&#x20;   COALESCE(\[PY Revenue per Product], 0)



RETURN

IF(

&#x20;   PrevYear = 0,

&#x20;   0,

&#x20;   DIVIDE(

&#x20;       \[YoY Revenue per Product],

&#x20;       PrevYear,

&#x20;       0

&#x20;   )

)





2\. Average Selling Price (ASP): {Total Sales ÷ Total Quantity Sold}



a. Average Selling Price =

DIVIDE(

&#x20;   \[Total Sales],

&#x20;   COUNTROWS(fact\_order\_items),

&#x20;   0

)



OR



Average Selling Price =

DIVIDE(

&#x20;   \[Total Sales],

&#x20;   \[Total Items Sold],

&#x20;   0

)





b. Average Selling Price % =

DIVIDE(

&#x20;   \[Average Selling Price],

&#x20;   CALCULATE(

&#x20;       \[Average Selling Price],

&#x20;       ALL(dim\_date)

&#x20;   ),

&#x20;   0

)





c. PY Average Selling Price =

CALCULATE(

&#x20;   \[Average Selling Price],

&#x20;   SAMEPERIODLASTYEAR(dim\_date\[date])

)





d. YoY Average Selling Price =

IF(

&#x20;   ISBLANK(\[PY Average Selling Price]),

&#x20;   BLANK(),

&#x20;   \[Average Selling Price] - \[PY Average Selling Price]

)



e. YoY % Average Selling Price =

VAR PrevYear =

&#x20;   COALESCE(\[PY Average Selling Price], 0)



RETURN

IF(

&#x20;   PrevYear = 0,

&#x20;   0,

&#x20;   DIVIDE(

&#x20;       \[YoY Average Selling Price],

&#x20;       PrevYear,

&#x20;       0

&#x20;   )

)







3\.  Average Order Value: 



a. Average Order Value =

DIVIDE(

&#x20;   \[Total Revenue],

&#x20;   \[Total Orders],

&#x20;   0

)



b. Average Order Value % =

DIVIDE(

&#x20;   \[Average Order Value],

&#x20;   CALCULATE(

&#x20;       \[Average Order Value],

&#x20;       ALL(dim\_date)

&#x20;   ),

&#x20;   0

)



c. PY Average Order Value =

CALCULATE(

&#x20;   \[Average Order Value],

&#x20;   SAMEPERIODLASTYEAR(dim\_date\[date])

)



d. YoY Average Order Value =

IF(

&#x20;   ISBLANK(\[PY Average Order Value]),

&#x20;   BLANK(),

&#x20;   \[Average Order Value] - \[PY Average Order Value]

)



e. YoY % Average Order Value =

VAR PrevYear =

&#x20;   COALESCE(\[PY Average Order Value], 0)



RETURN

IF(

&#x20;   PrevYear = 0,

&#x20;   0,

&#x20;   DIVIDE(

&#x20;       \[YoY Average Order Value],

&#x20;       PrevYear,

&#x20;       0

&#x20;   )

)





4\. Total Freight Cost:





a. Total Freight Cost =

SUM(fact\_order\_items\[freight\_value])



b. Total Freight Cost % =

DIVIDE(

&#x20;   \[Total Freight Cost],

&#x20;   CALCULATE(

&#x20;       \[Total Freight Cost],

&#x20;       ALL(dim\_date)

&#x20;   ),

&#x20;   0

)



c. PY Total Freight Cost =

CALCULATE(

&#x20;   \[Total Freight Cost],

&#x20;   SAMEPERIODLASTYEAR(dim\_date\[date])

)



d. YoY Total Freight Cost =

IF(

&#x20;   ISBLANK(\[PY Total Freight Cost]),

&#x20;   BLANK(),

&#x20;   \[Total Freight Cost] - \[PY Total Freight Cost]

)



e. YoY % Total Freight Cost =

VAR PrevYear =

&#x20;   COALESCE(\[PY Total Freight Cost], 0)



RETURN

IF(

&#x20;   PrevYear = 0,

&#x20;   0,

&#x20;   DIVIDE(

&#x20;       \[YoY Total Freight Cost],

&#x20;       PrevYear,

&#x20;       0

&#x20;   )

)







# Page-3. Order \& Payment Analysis:



kpis= {Completed Orders/ Cancelled Orders/ Payment Success Rate/ AVG Payment Value/ Average Payments per Order}



{AVG Delivery Days/ AVG Processing Hours}





1\. Completed Orders:



a. Completed Orders =

CALCULATE(

&#x20;   DISTINCTCOUNT(fact\_orders\[order\_id]),

&#x20;   fact\_orders\[order\_status] = "delivered"

)



b. Completed Orders % =

DIVIDE(

&#x20;   \[Completed Orders],

&#x20;   CALCULATE(

&#x20;       \[Completed Orders],

&#x20;       ALL(dim\_date)

&#x20;   ),

&#x20;   0

)



c. PY Completed Orders =

CALCULATE(

&#x20;   \[Completed Orders],

&#x20;   SAMEPERIODLASTYEAR(dim\_date\[date])

)



d. YoY Completed Orders =

IF(

&#x20;   ISBLANK(\[PY Completed Orders]),

&#x20;   BLANK(),

&#x20;   \[Completed Orders] - \[PY Completed Orders]

)



e. YoY % Completed Orders =

VAR PrevYear =

&#x20;   COALESCE(\[PY Completed Orders], 0)



RETURN

IF(

&#x20;   PrevYear = 0,

&#x20;   0,

&#x20;   DIVIDE(

&#x20;       \[YoY Completed Orders],

&#x20;       PrevYear,

&#x20;       0

&#x20;   )

)





2\. Cancelled Orders:



a. Cancelled Orders =

CALCULATE(

&#x20;   DISTINCTCOUNT(fact\_orders\[order\_id]),

&#x20;   fact\_orders\[order\_status] = "canceled"

)



b. Cancelled Orders % =

DIVIDE(

&#x20;   \[Cancelled Orders],

&#x20;   CALCULATE(

&#x20;       \[Cancelled Orders],

&#x20;       ALL(dim\_date)

&#x20;   ),

&#x20;   0

)



c. PY Cancelled Orders =

CALCULATE(

&#x20;   \[Cancelled Orders],

&#x20;   SAMEPERIODLASTYEAR(dim\_date\[date])

)



d. YoY Cancelled Orders =

IF(

&#x20;   ISBLANK(\[PY Cancelled Orders]),

&#x20;   BLANK(),

&#x20;   \[Cancelled Orders] - \[PY Cancelled Orders]

)



e. YoY % Cancelled Orders =

VAR PrevYear =

&#x20;   COALESCE(\[PY Cancelled Orders], 0)



RETURN

IF(

&#x20;   PrevYear = 0,

&#x20;   0,

&#x20;   DIVIDE(

&#x20;       \[YoY Cancelled Orders],

&#x20;       PrevYear,

&#x20;       0

&#x20;   )

)



3\. Payment Success Rate:



a. Payment Success Rate =

DIVIDE(

&#x20;   \[Completed Orders],

&#x20;   \[Total Orders],

&#x20;   0

)



b. Payment Success Rate % =

DIVIDE(

&#x20;   \[Payment Success Rate],

&#x20;   CALCULATE(

&#x20;       \[Payment Success Rate],

&#x20;       ALL(dim\_date)

&#x20;   ),

&#x20;   0

)



c. PY Payment Success Rate =

CALCULATE(

&#x20;   \[Payment Success Rate],

&#x20;   SAMEPERIODLASTYEAR(dim\_date\[date])

)



d. YoY Payment Success Rate =

IF(

&#x20;   ISBLANK(\[PY Payment Success Rate]),

&#x20;   BLANK(),

&#x20;   \[Payment Success Rate] - \[PY Payment Success Rate]

)



e. YoY % Payment Success Rate =

VAR PrevYear =

&#x20;   COALESCE(\[PY Payment Success Rate], 0)



RETURN

IF(

&#x20;   PrevYear = 0,

&#x20;   0,

&#x20;   DIVIDE(

&#x20;       \[YoY Payment Success Rate],

&#x20;       PrevYear,

&#x20;       0

&#x20;   )

)





4\. AVG Payment Value:



a. Average Payment Value =

DIVIDE(

&#x20;   \[Total Payment Value],

&#x20;   \[Total Orders],

&#x20;   0

)



b. Average Payment Value % =

DIVIDE(

&#x20;   \[Average Payment Value],

&#x20;   CALCULATE(

&#x20;       \[Average Payment Value],

&#x20;       ALL(dim\_date)

&#x20;   ),

&#x20;   0

)



c. PY Average Payment Value =

CALCULATE(

&#x20;   \[Average Payment Value],

&#x20;   SAMEPERIODLASTYEAR(dim\_date\[date])

)



d. YoY Average Payment Value =

IF(

&#x20;   ISBLANK(\[PY Average Payment Value]),

&#x20;   BLANK(),

&#x20;   \[Average Payment Value] - \[PY Average Payment Value]

)



e. YoY % Average Payment Value =

VAR PrevYear =

&#x20;   COALESCE(\[PY Average Payment Value], 0)



RETURN

IF(

&#x20;   PrevYear = 0,

&#x20;   0,

&#x20;   DIVIDE(

&#x20;       \[YoY Average Payment Value],

&#x20;       PrevYear,

&#x20;       0

&#x20;   )

)





5\. Average Payments per Order:



a. Average Payments per Order =

DIVIDE(

&#x20;   COUNTROWS(fact\_order\_payments),

&#x20;   \[Total Orders],

&#x20;   0

)



OR



Average Payments per Order =

DIVIDE(

&#x20;   \[Total Payment Transactions],

&#x20;   \[Total Orders],

&#x20;   0

)





b. Average Payments per Order % =

DIVIDE(

&#x20;   \[Average Payments per Order],

&#x20;   CALCULATE(

&#x20;       \[Average Payments per Order],

&#x20;       ALL(dim\_date)

&#x20;   ),

&#x20;   0

)





c. PY Average Payments per Order =

CALCULATE(

&#x20;   \[Average Payments per Order],

&#x20;   SAMEPERIODLASTYEAR(dim\_date\[date])

)



d. YoY Average Payments per Order =

IF(

&#x20;   ISBLANK(\[PY Average Payments per Order]),

&#x20;   BLANK(),

&#x20;   \[Average Payments per Order] - \[PY Average Payments per Order]

)



e. YoY % Average Payments per Order =

VAR PrevYear =

&#x20;   COALESCE(\[PY Average Payments per Order], 0)



RETURN

IF(

&#x20;   PrevYear = 0,

&#x20;   0,

&#x20;   DIVIDE(

&#x20;       \[YoY Average Payments per Order],

&#x20;       PrevYear,

&#x20;       0

&#x20;   )

)







# Page-4. Customer Behavior Analysis:



\## Revenue per Customer and Average Customer Spend use the same calculation:



(Total Revenue ÷ Total Customers) use only one best KPI





Kpis= {Revenue per Customer/ Average Orders per Customer/ Average Customer Spend/ ~~Active Customers (selected period)~~/ New Customers/ Repeat Customer Rate/ Customer Retention Rate/ YoY Customer Growth} 







1\. Revenue per Customer:



a. Revenue per Customer =

DIVIDE(

&#x20;   \[Total Revenue],

&#x20;   \[Total Customers],

&#x20;   0

)





b. Revenue per Customer % =

DIVIDE(

&#x20;   \[Revenue per Customer],

&#x20;   CALCULATE(

&#x20;       \[Revenue per Customer],

&#x20;       ALL(dim\_date)

&#x20;   ),

&#x20;   0

)





c. PY Revenue per Customer =

CALCULATE(

&#x20;   \[Revenue per Customer],

&#x20;   SAMEPERIODLASTYEAR(dim\_date\[date])

)



d. YoY Revenue per Customer =

IF(

&#x20;   ISBLANK(\[PY Revenue per Customer]),

&#x20;   BLANK(),

&#x20;   \[Revenue per Customer] - \[PY Revenue per Customer]

)



e. YoY % Revenue per Customer =

VAR PrevYear =

&#x20;   COALESCE(\[PY Revenue per Customer], 0)



RETURN

IF(

&#x20;   PrevYear = 0,

&#x20;   0,

&#x20;   DIVIDE(

&#x20;       \[YoY Revenue per Customer],

&#x20;       PrevYear,

&#x20;       0

&#x20;   )

)







2\. Average Orders per Customer:



a. Average Orders per Customer =

DIVIDE(

&#x20;   \[Total Orders],

&#x20;   \[Total Customers],

&#x20;   0

)



b. Average Orders per Customer % =

DIVIDE(

&#x20;   \[Average Orders per Customer],

&#x20;   CALCULATE(

&#x20;       \[Average Orders per Customer],

&#x20;       ALL(dim\_date)

&#x20;   ),

&#x20;   0

)



c. PY Average Orders per Customer =

CALCULATE(

&#x20;   \[Average Orders per Customer],

&#x20;   SAMEPERIODLASTYEAR(dim\_date\[date])

)



d. YoY Average Orders per Customer =

IF(

&#x20;   ISBLANK(\[PY Average Orders per Customer]),

&#x20;   BLANK(),

&#x20;   \[Average Orders per Customer] - \[PY Average Orders per Customer]

)



e. YoY % Average Orders per Customer =

VAR PrevYear =

&#x20;   COALESCE(\[PY Average Orders per Customer], 0)



RETURN

IF(

&#x20;   PrevYear = 0,

&#x20;   0,

&#x20;   DIVIDE(

&#x20;       \[YoY Average Orders per Customer],

&#x20;       PrevYear,

&#x20;       0

&#x20;   )

)





3\. Average Customer Spend:



a. Average Customer Spend =

DIVIDE(

&#x20;   \[Total Revenue],

&#x20;   \[Total Customers],

&#x20;   0

)



b. Average Customer Spend % =

DIVIDE(

&#x20;   \[Average Customer Spend],

&#x20;   CALCULATE(

&#x20;       \[Average Customer Spend],

&#x20;       ALL(dim\_date)

&#x20;   ),

&#x20;   0

)



c. PY Average Customer Spend =

CALCULATE(

&#x20;   \[Average Customer Spend],

&#x20;   SAMEPERIODLASTYEAR(dim\_date\[date])

)



d. YoY Average Customer Spend =

IF(

&#x20;   ISBLANK(\[PY Average Customer Spend]),

&#x20;   BLANK(),

&#x20;   \[Average Customer Spend] - \[PY Average Customer Spend]

)



e. YoY % Average Customer Spend =

VAR PrevYear =

&#x20;   COALESCE(\[PY Average Customer Spend], 0)



RETURN

IF(

&#x20;   PrevYear = 0,

&#x20;   0,

&#x20;   DIVIDE(

&#x20;       \[YoY Average Customer Spend],

&#x20;       PrevYear,

&#x20;       0

&#x20;   )

)







4\. New Customers: need to create calc col and then implement logic



\## Calculated Column:  (First Purchase Date / Last Purchase Date)



First Purchase Date =

CALCULATE(

&#x20;   MIN(fact\_orders\[order\_purchase\_date]),

&#x20;   RELATEDTABLE(fact\_orders)

)





Last Purchase Date =

CALCULATE(

&#x20;   MAX(fact\_orders\[order\_purchase\_date]),

&#x20;   RELATEDTABLE(fact\_orders)

)





Customer Tenure (Days) =

DATEDIFF(

&#x20;   dim\_customer\[First Purchase Date],

&#x20;   dim\_customer\[Last Purchase Date],

&#x20;   DAY

)





Customer Type =

IF(

&#x20;   dim\_customer\[Total Orders] = 1,

&#x20;   "New",

&#x20;   "Returning"

)





Returning Customers =

COUNTROWS(

&#x20;   FILTER(

&#x20;       VALUES(dim\_customer\[customer\_id]),

&#x20;       CALCULATE(DISTINCTCOUNT(fact\_orders\[order\_id])) > 1

&#x20;   )

)







a. New Customers =

CALCULATE(

&#x20;   DISTINCTCOUNT(dim\_customer\[customer\_id]),

&#x20;   USERELATIONSHIP(

&#x20;       dim\_customer\[First Purchase Date],

&#x20;       dim\_date\[date]

&#x20;   )

)





b. New Customers % =

DIVIDE(

&#x20;   \[New Customers],

&#x20;   CALCULATE(

&#x20;       \[New Customers],

&#x20;       ALL(dim\_date)

&#x20;   ),

&#x20;   0

)



c. PY New Customers =

CALCULATE(

&#x20;   \[New Customers],

&#x20;   SAMEPERIODLASTYEAR(dim\_date\[date])

)



d. YoY New Customers =

IF(

&#x20;   ISBLANK(\[PY New Customers]),

&#x20;   BLANK(),

&#x20;   \[New Customers] - \[PY New Customers]

)



e. YoY % New Customers =

VAR PrevYear =

&#x20;   COALESCE(\[PY New Customers], 0)



RETURN

IF(

&#x20;   PrevYear = 0,

&#x20;   0,

&#x20;   DIVIDE(

&#x20;       \[YoY New Customers],

&#x20;       PrevYear,

&#x20;       0

&#x20;   )

)







5\. Repeat Customer Rate (Customer Retention Rate): (Returning Customers ÷ Total Customers × 100)





a. Repeat Customer Rate =

DIVIDE(

&#x20;   \[Returning Customers],

&#x20;   \[Total Customers],

&#x20;   0

)



b. Repeat Customer Rate % =

DIVIDE(

&#x20;   \[Repeat Customer Rate],

&#x20;   CALCULATE(

&#x20;       \[Repeat Customer Rate],

&#x20;       ALL(dim\_date)

&#x20;   ),

&#x20;   0

)



c. PY Repeat Customer Rate =

CALCULATE(

&#x20;   \[Repeat Customer Rate],

&#x20;   SAMEPERIODLASTYEAR(dim\_date\[date])

)



d. YoY Repeat Customer Rate =

IF(

&#x20;   ISBLANK(\[PY Repeat Customer Rate]),

&#x20;   BLANK(),

&#x20;   \[Repeat Customer Rate] - \[PY Repeat Customer Rate]

)



e. YoY % Repeat Customer Rate =

VAR PrevYear =

&#x20;   COALESCE(\[PY Repeat Customer Rate], 0)



RETURN

IF(

&#x20;   PrevYear = 0,

&#x20;   0,

&#x20;   DIVIDE(

&#x20;       \[YoY Repeat Customer Rate],

&#x20;       PrevYear,

&#x20;       0

&#x20;   )

)





6\. YoY Customer Growth:



a. Customer Growth (use the "Total Customers" KPI)





b. Customer Growth % =

DIVIDE(

&#x20;   \[Total Customers],

&#x20;   CALCULATE(

&#x20;       \[Total Customers],

&#x20;       ALL(dim\_date)

&#x20;   ),

&#x20;   0

)



c. PY Customer Growth =

CALCULATE(

&#x20;   \[Total Customers],

&#x20;   SAMEPERIODLASTYEAR(dim\_date\[date])

)





d. YoY Customer Growth =

IF(

&#x20;   ISBLANK(\[PY Customer Growth]),

&#x20;   BLANK(),

&#x20;   \[Total Customers] - \[PY Customer Growth]

)



e. YoY % Customer Growth =

VAR PrevYear =

&#x20;   COALESCE(\[PY Customer Growth], 0)



RETURN

IF(

&#x20;   PrevYear = 0,

&#x20;   0,

&#x20;   DIVIDE(

&#x20;       \[YoY Customer Growth],

&#x20;       PrevYear,

&#x20;       0

&#x20;   )

)







# Page-5. Product Performance Analysis:







