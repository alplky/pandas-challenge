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
-

### Age Demographics
- 

### Purchasing Analysis (Age)
- 

### Top Spenders
- 

### Most Popular Items 
- 

### Most Profitable Items 
-
