Import vs DirectQuery

Import Mode:

Data is loaded and stored inside Power BI.
Reports are generally faster.
Data needs to be refreshed to get the latest changes.
Good for small to medium-sized datasets.
Most DAX functions and Power BI features are available.

DirectQuery Mode:

Data remains in the source database.
Power BI sends queries to the database whenever data is needed.
Data is more up-to-date without importing the entire dataset.
Performance depends on the database and network.
Some DAX functions and features have limitatio




<!-- formula to appned data -->
in custome coulumn --  Excel.Workbook([Content])


<!-- formula to merge two columns  -->
in custom column
[CONTACTFIRSTNAME]&" "&[CONTACTLASTNAME]


<!-- dax formula-- sum and sums -->
<!--                SUM      -->
implicit = when you get direct total using card
explicit=
1. right click on table and select new measure
2. a formula bar will open write Measure = SUM('Sales_Data1'[QUANTITYORDERED]) and press enter
3. you could see a column is increased in the table and now use card and drag that column in card feild and see total on card
We are using explicit bcz we can make changes in quantity of card using 
dq=[measure]*2    "measure is the total value obtained above in card"

<!-- SUMX -->
everything is done same but the diff is ex u want to calculate price of taotal items you bought so that is u will multiply price* quantity and then will sum all of them for this we use sumx
<!-- formula -->
Total_sales=SUMX('Sales_Data1',Sales_Data1[QUANTITYORDERED]*Sales_Data1[PRICEEACH])


<!-- TO ADD NEW COLUMN IN TABLE BY CALCULATING SOME VALUE -->
right click on table click on add column and then write this formula on topp 
sales amount = Sales_Data1[QUANTITYORDERED]*Sales_Data1[PRICEEACH]

<!-- TOGET YEAR FROM DATE OF BIRTH -->
add new column  Year=YEAR(Employee_Data[Date of Birth])
for weekday  -- weekday=weekday(employee_data[date_of_birth].[date],1)    // 1 2 3 are three ways of geeting weekdays like from when to start monday=1 in case 1 , mondat =0 in case 2, sunday =1 in case 3

<!-- to get dayname -->
dayname=format(employee_data[date_of_birth].[date],"DDDD") 
<!-- to get monthname -->
dayname=format(employee_data[date_of_birth].[date],"MMMM")

<!-- to get weeknum -->
weeknum=weeknum(employee_data[date_of_birth].[date],1)
<!-- to get endofmonth basically last date of month ie 30 or 31 -->
endofmonth=eomonth(employee_data[date_of_birth].[date],1)  1 like after oct you want for nov , 2 after oct you want for after 2 months

<!-- TO CALC AGE OF EMPLOYEE --> FIRST year bale column ko sep krna h dob se line 52 year bala formula then
age=DATEDIFF(Employee_Data[Date of Birth].[Date],TODAY(),YEAR)

<!--  to get from how many years is he working -->
Tenure=DATEDIFF(Employee_Data[Date of joining].[Date],TODAY(),YEAR)

<!-- to sum a row -->
Total_sales_amount = sum('TechyStore Sales_Data'[Total Sale (INR)])


<!-- TO CALC SALES PERCENTAGE WRT ONE PRODUCT -->
<!-- to get the same vakue in each line from one of the product like we have camera food car now i wabt new row where in each line the prices 
of camera should be there only inorder to calc something like percentage wtih respect to camera  -->
Camera_Sales=CALCULATE([Total_sales_amount],'TechyStore Sales_Data'[Product]="Camera")
Per_camera = [Total_sales_amount]/[Camera_Sales]


<!-- if you have calc total now you want that total to come in another column and every row then -->
totalsalesamt=CALCULATE([Total_sales_amount],ALL('TechyStore Sales_Data'[Product]))
perwithtotal = [Total_sales_amount]/[totalsalesamt]

<!-- to calc 10 days data from any date to ay date -->
10_dayssales=CALCULATE([Total_sales_amount],DATESBETWEEN('TechyStore Sales_Data'[Sales Date].[Date],DATE(2023,10,1),DATE(2023,10,10)))
can do using slicer by shifting dates in that as well

<!-- to calculate mtd -->
<!-- first you have to seperate oyt date in diff table by using transform and creating blank query and writing this in formula bar
= List.Dates(#date(2023,1,1),731,#duration(1,0,0,0)) -->
<!-- then after that sep year date day by using add column and then close and apply and then do this formula to get mtd -->
MTD = TOTALMTD([Total_sales_amount],Query1[Date].[Date])

<!-- month wise total -->
QTD = TOTALQTD([Total_sales_amount],Query1[Date].[Date])

YTD = TOTALYTD([Total_sales_amount],Query1[Date].[Date])

M = Month → MTD = This month's performance so far
Q = Quarter → QTD = This quarter's performance so far
Y = Year → YTD = This year's performance so far