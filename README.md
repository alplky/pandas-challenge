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
- 

### Top Spenders
- 

### Most Popular Items 
- 

### Most Profitable Items 
-
