# Online Retail Data Analysis With Excel

## Table of Contents
### Introduction
### About Data
### Data Cleaning and Preparation
### The Analysis
### Findings
### Data Visualization
### Recommendation

### INTRODUCTION
The major purpose of this analysis is to categorize products into different groups based on the value they bring to the business in order to drive customer satisfaction and reduce company loss. To do this effectively, I will borrow ideas from the RFM model for customer segmentation to perform this analysis. The RFM analysis will be applied to score products based on how recently they been sold, how frequently they are were sold and the total quantity sold. Based on this scores, each product will be categorized into a group. 
This type of analysis is very useful for dealing with overstocking and understocking of products. With the knowledge of how products perform, business owners can take proactive measures to ensure that they don't run out of high selling products, they will be able to identify products that may need promotional marketing, it is also a great way to reduce stock expiration and also to assign strategic location to each product in the store.
This analysis will also look at how the store is being patronized across different countries.
There will be a visual representation of my findings and recommendations will be given at the end of the analysis.

### ABOUT DATA
This data was downloaded from kaggle.com, an online communitiy for Data professionals. The data contains 8 columns and 541,911 rows. The 8 columns in this dataset are InvoiceNo, StockCode, Description, Quantity, InvoiceDate, Unit Price, Customer Id and Country.

### DATA CLEANING AND PREPARATION
It is almost impossible to find any dataset without quality issues, so it is good practice to always check for quality issues and mitigate them before proceeding with your analysis as bad data can have extremely unpleasant effects on a business.
To ensure that I have a clean data for my analysis, I inserted my data into a pivot table to have a better understanding of the data, then I applied the sort and filter function on each column to have a closer inspection of each column, starting with the Invoice Number column. Here is a copy of the dataset before the cleaning was done.
[Online Retail.xlsx](https://github.com/kelechiogbogu/online_retail/files/9227674/Online.Retail.xlsx)
Before I started the cleaning process, I made a copy of my dataset and renamed it following the file naming convention.

InvoiceNo: A glance at this column reveals that the values are numerical values of a length of 6. However, when I applied the sort function, I found some alpha-numeric values made up of 7 characters. The numeric values were assinged to completed transactions while the alphanumerics were used for backorders. 
Then I used the IF, AND formular to Assign Either Valid and invalid to rows that meet the character length criteria and rows that did not respectively. I created a temporary column, InvoiceCheck for this.
![IF AND FOR INVOICE ID CHECK](https://user-images.githubusercontent.com/95935148/182002353-4279bdc3-5536-47bc-baed-a7be84cf96d4.PNG)
I filtered out all the rows with valid invoice Id, just to have a view of those with invalid ID before deleting them. One row was found and deleted.

StockCode: With the help of pivot table, sort and filter functions, I found that some rows contain some other codes for business datails rather than products; details such as Amazon fees, bankcharges, and other logistics information. Since I am only interested in the products for this analysis, those rows were deleted. I also checked for blanks and found none.
 
 Description: This is one of the most relevant columns for this analysis, this coulmn contains description of the products. First, I ensured all missings rows were removed.(This is a fictional situation, hence the immediate removal. In a real life situation, I will find ways of getting the appropriate data for these rows, e.g going back to the sales department, looking for copies of invoices etc).
I used the pivot table to have a closer look at this column and found some invalid and irrelevant inputs such as ?, ??, ?missing, CRUX commission, ?sold as sets?, ??missing, ???, ?????damages, ?????missing, ????lost, check, damaged, cracked, crushed, faulty, found, Next day carriage, parking charge etc, I went ahead and deleted them. What most of these rows have in common is that they all have a unit price of 0.

Quantity: This is another very important column for this analysis. It cotains the number of items sold at each transaction. Recall that the dataset contains both completed transactions and back orders (This observation was made when cleaning the InvoiceNo column). The invoice numbers of all back orders are alphanumeric values that are of a length of 7 while the completed transactions have numeric Invoice numbers of length 6. The quantity of all back orders are stored with negative numbers while that of completed transactions are stored with positive numbers. Having this at the back of my mind, I applied conditional formatting to my Invoice number column, I formatted the cells of InvoiceNo that are equal to a character length of 6 with green(these are rows that contained completed order)and formatted the cells of the invoiceNo that are equal to a character length of 7 with red(they contain back orders).
I used the filter function to pull out rows with green cells and then applied the IF formular to check for negative numbers in the Quantity column, I created a temporary column for this.
![NEGATIVE CHECK](https://user-images.githubusercontent.com/95935148/182002535-d61323a7-200b-4515-9e23-2786b240a49c.PNG)
Then I used the filter function on the NegativeCheck column (the temporary column I created) to pull out all invalids, 16 rows were found and the description column of the 16 rows further showed that the rows contained some irelevant data. 
![NEGATIVE CHECK FILTER RESULT](https://user-images.githubusercontent.com/95935148/182002653-9f5c3bac-c010-4be3-9393-de215e59077f.PNG)
They were all deleted.
I applied the same steps in checking for quantities stored as positive numbers in the back order rows, a few rows were found and deleted.

InvoiceDate: I found no issues with this column.

UnitPrice: I formatted the unit price column as currency. I also checked for any unit price that is less than or equal to 0 using the IF formular.
I found some rows and deleted them.

CustomerId: Blanks were found and replaced with Not Specified. This was done using the Find and Replace function.

Country: Some countries were unspecified but this will not pose any problem to the analysis, so it was ignored.

CHECKING FOR DUPLICATES: After going through all my columns one after the other, I checked for duplicates by creating a unique Id column which I called UID and filled it using the concatenate formular to join all values, this is because my data has no unique column and also because I wanted to have a view of the duplicate rows before deleting them. After the concatenation, I applied distinct colors to the unique and duplicate rows, then I filtered by color and deleted all duplicates.
![dPLICATE VALUES CHAECK](https://user-images.githubusercontent.com/95935148/182002726-1c7c9f26-ff1c-41a5-85b3-b67a4440f301.PNG)
An easier and faster way to do this is by using the remove duplicate function.  

### THE ANALYSIS
Firstly, I created a new column(DaysSinceLastSold), to populate this column, I used the most recent date from the InvoiceDate column as the comparison date, then I went ahead to subtract each date from the comparison date. This will be neccesary when grouping the products.

For the product categorization, I needed to work with only sales that were completed, so I applied filter on the dataset and copied only data for completed orders, to a new worksheet. I inserted it into a pivot table, used Description as the rows and then DaysSinceLastBought(min), Quantity(count) and Quantiy(Sum) as Values. Then based on specified criteria, each product was scored on a scale of 1-5. All products were further categorized into five groups. There are many formulars used for setting criteria for scoring and categorization e.g tertiles, quartiles, quintiles, percentiles etc. However, for this analysis, the criteria was set based on subject matter knowledge. I used numbers 1-5 to categorize the products based on when it was last sold,
5 was assigned to products sold in the last 1-15 days,
4 to products sold in the last 16 - 30 days
3 to products sold in the last 31 - 90 days
2 to products sold in the last 91 - 180 days
1 to products slod in the last 181 - max day.
This was done using the IFS formular =IFS(B20>180,1,AND(B20<=180,B20>90),2,AND(B20<=90,B20>30),3,AND(B20<=30,B20>15),4,AND(B20<=15,B20>=0),5)
See file:
[ProductCategory_Pivot.xlsx](https://github.com/kelechiogbogu/online_retail/files/9227712/ProductCategory_Pivot.xlsx)

A new column(Total Revenue) was added to calculate how much each product generates. I populated this column by multiplying the Unit Price by the quantity. This was used the find the products that generated the highest revenue.

See a copy of my clean and updated data:
[OnlineRetailDataset_2010-2011.zip](https://github.com/kelechiogbogu/online_retail/files/9227720/OnlineRetailDataset_2010-2011.zip)

### FINDINGS
After categorizing the products into High Selling, Above Average, Average, Below Average and Low Selling, I found out that 55% percent of the products fall under the  Average products, 19% pecrcent are Low Selling products, while High Selling products make up only 4% percent of the products.
91% of the products were puurchased from customers in the United kingdom, however, Germany and France seems to have a some potentials.
Regency Casket and 3 Tier is the highest bought product, it also recorded the highest number of back orders by frequency.
In 2011, most of the back orders happened in October.

### DATA VIZ
Insights from the dataset were plotted into charts for easier understanding. 
![DAshboard](https://user-images.githubusercontent.com/95935148/182003173-9b0e54fa-a0cd-49ce-96b1-e8c80c5701c2.PNG)
Open file to see full dashboard:
[OnlineRetailDashboard_2010-2011.xlsx](https://github.com/kelechiogbogu/online_retail/files/9227728/OnlineRetailDashboard_2010-2011.xlsx)

### RECOMMENDATION
* Promotional Sales should be conducted for products in the low selling category, this shouldn't be done blindly as products may fall in this category for numerous reason, eg it could be as a result of seasonal demand.
* Managers should ensure that products in the high scoring category are always avaliable for purchase, this will reduce the rate of back orders.
* Brand awareness campaigns should be organized in countries that recorded low sales.
* Managers should pay attention to products that received the highest back orders and stock up on those products to prevent future occurence. Product unavaliability leads to customer dissatisfaction.
* It is important to find out the reason for the low sales of some products, this will help determine what actions should be taken towards those products.

### LIMITATION
The major limitation faced is the unavaliablity of profit information or means of finding profit in the dataset, this would have been one of the basis for categorizing products in order to reveal the value they bring to the business.








