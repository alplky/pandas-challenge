# pandas-challenge

## Overview
Hereos of Pymoli is a free, online fantasy game where players are encouraged to buy additional items to enhance their gaming experience. In order to better understand how players are utilizing in-game purchase options, recent purchasing data has been broken down into a concise report.

## Observable Trends and Insights
Players between the ages of 20 - 24 make up almost half of the total player count at 44.5%. This same age group also accounts for close to half of the total purchase count with a total purchase value of $1,114.06. Gender demographics show that male players comprise the overwhelming majoriy of players at 84.03%; out of a total of 576 players, 484 players identify as male. While it appears that Heroes of Pymoli is most popular amoung college aged males, they do not spend the most per purchase on average -- female players spend $4.47 on average per purchase while male players spend $4.07. Targeting ads of Heroe of Pymoli towards females players between the ages of 20-24 could significantly increase revenue if female players were at the same count level as male players. 

## Table Breakdowns:
### Player Count
- Total players was caluculated using .nunique() on the SN(screen name) column to account for the unique players who have made purchases. This was then passed into a data frame for display output. 

### Purchasing Analysis (Total)
- The number of unique items was counted by using .nunique() on the Item ID column.
- The average price was calulcated by using .mean() on the Price column and rounding to 2 decimal places. 
- Total purchase was caluculated by using .count() on the Purchase ID column.
- Total revenue was done by using .sum() on the Price column. 
- Each calulcaion was assinged to a variable, then passed into a data frame and formatting with f-strings for display output. 

### Gender Demograhics
- In order to caluculate gender demographics, a new data frame was made consistig of the SN and Gender columns. Then .dropduplicates() was used with the SN column to assure only individual players were being counted in the analysis by gender. 
- The gender count was achievied by grouping and counting by the Gender row. 
- Each gender percentage was accounted for by dividing the gender count by the sum of the gender count, and rounding to two decimal places. 
- The calulcations were assinged to variables and passed to a data frame. The data frame was then formatted using .style.format() to add the percentage symbols to the rows in the percentage column. 

### Purchasing Analysis (Gender)
- Total purchases by gender were counted by grouping by the Gender column and using .count().
- The total purchase value was calulcated by grouping by the Gender column and using .sum() on the Price column. 
- Each caluclation was then assinged to a variable. 
- To get the average purchase price by gender, the total purchase value was divided by the total count of gender purchases and rounded to 2 decimal places. 
- The average total purchase per person in each gender group was calculated by diving the total purchase value by the unique gender count that was created for the Gender Demographics table, then rounded to 2 decimal places. 
- The calculations for averages were both assigned to variables. 
- All variables were then passed to a data frame for display output. The data frame was formated with .style.format() to add dollar signs to all of the rows for columns with monetary values. 

### Age Demographics
- To create age ranges, pd.cut() was used and a new column "Age Ranges" was passed back into the data frame. Bins were used in increments of 4 years, from 0 to 45 (the max age in the dataset). Labels were created to accompany the respective bins. 
- A new dataframe was created out of columns SN, Age Range, and Age from the original data frame. Then repeating screen names were removed with .dropduplicates() to account for each player only once. 
- Age count was calculated by grouping by the Age Range column and using .count() on the Age column.
- The percent of players in each age range was calculated by diving the age count by the sum of the age count, multiplying by 100 and rounding to 2 decimal places. 
- Each calculation was assined to a variable. 
- The variables were then passed to a data frame for display output. The data frame was then formatted to add a percentage symbol to the rows in the percentage column. 

### Purchasing Analysis (Age)
- The purchase count by age range was calculated by grouping by the Age Range column and using .count() on the Purchase ID column.
- Total purchase value was calculated by grouping by the Age Range column and using .sum() on the Price column. 
- Both calculations were then assigned to variables. 
- The average price for each gender range was calculated by diving the total purchase by the purchase count and rounding to 2 decimal points. 
- In order to calculate the average total purchase per person in each age range, first a variable was created by grouping by the Age Range column and counting the unique values of the SN column using .nunique(). The average was then calulated by dividing the total purchase value by the unique user count within each age range. 
- The variables were then passed into a dataframe for display output. The data frame was formatted using .style.format() to add dollar signs to all rows within columns that contained monetary values.  

### Top Spenders
- The purchase count for each player was calculated by grouping by the SN column and using .count() on the Purchase ID column. 
- The total purchase per person was calculated by grouping by the SN column and using .sum() on the Price column. 
- Both calculations were then passed to variables. 
- The average purchase price per player was calculated by diving the total purchase per person by the total purchase count per person, then rounding to 2 decimal points. 
- The variables were then passed to a data frame for display output and sorted using .sort_values(), in descending order, by Total Purchase Value. Then, .head(5) was used to dispaly the top 5 spenders. The data frame was formatted using .style.format() to add dollar signs to the rows with columns containing monetary values. 

### Most Popular Items 
- To analyze the most popular items, a data frame was created out of the columns Item ID, Item Name, and Price from the original data frame. 
- The purchase count was calulated by grouping by the Item ID and Item Name columns and using .count() on the Item ID column.
- The item price was assigned to a variable by grouping by the Item ID and Item Name columns and using .mean() on the Price column. 
- The total purchase value was calculated by grouping by the Item ID and Item Name columns and using .sum() on the Price column. 
- The calculations were then assinged to variables. 
- The variables were then passed to a data frame for display output and sorted using .sort_values(), in descending order, by Purchase Count. To get the top 5 most popular items, .head(5) was used. The data frame was then formatted using .style.format() to add dollar signs to all rows in columns with monetary values. 

### Most Profitable Items 
- The most profitable items table was created by reusing the Popular Items data frame and sorting by Total Purchase Value in descending order with .head(5). The dat frame was then formatted using .style.format() to add dollar signs to all rows in columns with monetary values.
