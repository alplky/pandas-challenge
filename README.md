# pandas-challenge

## Overview
Heroes of Pymoli is a free, online fantasy game where players are encouraged to buy additional items to enhance their gaming experience. To better understand how players are utilizing in-game purchase options, recent purchasing data has been broken down into a concise report.

## Observable Trends and Insights
Players between the ages of 20 - 24 make up almost half of the total player count at 44.5%. This same age group also accounts for close to half of the total purchase count with a total purchase value of $1,114.06. Gender demographics show that male players comprise the overwhelming majority of players at 84.03%; out of a total of 576 players, 484 players identify as male. 

While it appears that Heroes of Pymoli is most popular among college-aged males, they do not spend the most per purchase on average -- female players spend $4.47 on average per purchase while male players spend $4.07. Targeting ads of Heroe of Pymoli towards females players between the ages of 20-24 could significantly increase revenue if female players were at the same count level as male players. 

## Table Breakdowns:
### Player Count
- Total players was calculated using .nunique() on the SN(screen name) column to account for the unique players who have made purchases. This was then passed into a data frame for display output.
```python
total_players_df = pd.DataFrame({
    "Total Players": [df["SN"].nunique()]
})
```

### Purchasing Analysis (Total)
- The number of unique items was counted by using .nunique() on the Item ID column.
- The average price was calculated by using .mean() on the Price column and rounding to 2 decimal places.
- Total purchase was calculated by using .count() on the Purchase ID column.
- Total revenue was done by using .sum() on the Price column.
- Each calculation was assigned to a variable, then passed into a data frame and formatting with f-strings for display output.
```python
unique_items = df["Item ID"].nunique()
avg_price = round(df["Price"].mean(), 2)
total_purchases = df["Purchase ID"].count()
total_revenue = df["Price"].sum()

purchase_analysis_df = pd.DataFrame({
    "Number of Unique Items": [unique_items],
    "Average Price" : [(f"${avg_price}")],
    "Number of Purchases": [total_purchases],
    "Total Revenue" : [(f"${total_revenue}")]
})
```

### Gender Demograhics
- To calculate gender demographics, a new data frame was made consisting of the SN and Gender columns. Then .dropduplicates() was used with the SN column to assure only individual players were being counted in the analysis by gender.
- The gender count was achieved by grouping and counting by the Gender row.
- Each gender percentage was accounted for by dividing the gender count by the sum of the gender count and rounding to two decimal places.
- The calculations were assigned to variables and passed to a data frame. The data frame was then formatted using .style.format() to add the percentage symbols to the rows in the percentage column.

```python
gender_df = df[["SN", "Gender"]]
gender_df = gender_df.drop_duplicates(subset=["SN"])

unique_gender_count = gender_df.groupby(["Gender"])["Gender"].count()

gender_percent = round(unique_gender_count / unique_gender_count.sum() * 100, 2)

gender_dems = pd.DataFrame({
    "Total Count": unique_gender_count,
    "Percentage of Players": gender_percent
})

gender_dems.style.format({"Percentage of Players": "{:.2f}%"})
```

### Purchasing Analysis (Gender)
- Total purchases by gender were counted by grouping by the Gender column and using .count().
- The total purchase value was calculated by grouping by the Gender column and using .sum() on the Price column.
- Each calculation was then assigned to a variable.
- To get the average purchase price by gender, the total purchase value was divided by the total count of gender purchases and rounded to 2 decimal places.
- The average total purchase per person in each gender group was calculated by diving the total purchase value by the unique gender count that was created for the Gender Demographics table, then rounded to 2 decimal places.
- The calculations for averages were both assigned to variables.
- All variables were then passed to a data frame for display output. The data frame was formated with .style.format() to add dollar signs to all of the rows for columns with monetary values.

```python
gender_purchases = df.groupby(["Gender"])["Gender"].count()

gender_total = df.groupby(["Gender"])["Price"].sum()

gender_avg = round(gender_total / gender_purchases, 2)

per_person_gender = round((gender_total / unique_gender_count), 2)

purchase_gender_df = pd.DataFrame({
    "Purchase Count": gender_purchases,
    "Average Purchase Price": gender_avg,
    "Total Purchase Value": gender_total,
    "Avg Total Purchase per Person": per_person_gender
})

purchase_gender_df.style.format({"Average Purchase Price": "${:,.2f}", 
                          "Total Purchase Value": "${:,.2f}",
                          "Avg Total Purchase per Person": "${:,.2f}"})
```

### Age Demographics
- To create age ranges, pd.cut() was used and a new column "Age Ranges" was passed back into the data frame. Bins were used in increments of 4 years, from 0 to 45 (the max-age in the dataset). Labels were created to accompany the respective bins.
- A new data frame was created out of columns SN, Age Range, and Age from the original data frame. Then repeating screen names were removed with .dropduplicates() to account for each player only once.
- Age count was calculated by grouping by the Age Range column and using .count() on the Age column.
- The percent of players in each age range was calculated by diving the age count by the sum of the age count, multiplying by 100, and rounding to 2 decimal places.
- Each calculation was assigned to a variable.
- The variables were then passed to a data frame for display output. The data frame was then formatted to add a percentage symbol to the rows in the percentage column.

```python
df["Age Range"] = pd.cut(
    df["Age"], 
    bins = [0, 9, 14, 19, 24, 29, 34, 39, 45],
    labels = ["<10", "10-14", "15-19", "20-24", "25-29", "30-34", "35-30", "40+"]
)

age_dems_df = df[["SN", "Age Range", "Age"]]
age_dems_df = age_dems_df.drop_duplicates(subset=["SN"])

age_count = age_dems_df.groupby(["Age Range"])["Age"].count()

age_percent = round(age_count / age_count.sum() * 100, 2)

age_df = pd.DataFrame({
    "Total Count": age_count,
    "Percentage of Players": age_percent
})

age_df.style.format({"Percentage of Players": "{:.2f}%"})
```

### Purchasing Analysis (Age)
- The purchase count by age range was calculated by grouping by the Age Range column and using .count() on the Purchase ID column.
- Total purchase value was calculated by grouping by the Age Range column and using .sum() on the Price column.
- Both calculations were then assigned to variables.
- The average price for each gender range was calculated by diving the total purchase by the purchase count and rounding to 2 decimal points.
- In order to calculate the average total purchase per person in each age range, first, a variable was created by grouping by the Age Range column and counting the unique values of the SN column using .nunique(). The average was then calculated by dividing the total purchase value by the unique user count within each age range.
- The variables were then passed into a data frame for display output. The data frame was formatted using .style.format() to add dollar signs to all rows within columns that contained monetary values.

```python
purchase_count = df.groupby(["Age Range"])["Purchase ID"].count()

total_purchase = df.groupby(["Age Range"])["Price"].sum()

avg_price = round(total_purchase / purchase_count, 2)

user_age = df.groupby(["Age Range"])["SN"].nunique()

avg_total = round(total_purchase / user_age, 2)

purchase_age = pd.DataFrame({
    "Purchase Count": purchase_count,
    "Average Purchase Price": avg_price,
    "Total Purchase Value": total_purchase,
    "Avg Total Purchase per Person": avg_total
})

purchase_age.style.format({"Average Purchase Price": "${:,.2f}", 
                          "Total Purchase Value": "${:,.2f}",
                          "Avg Total Purchase per Person": "${:,.2f}"}) 
```

### Top Spenders
- The purchase count for each player was calculated by grouping by the SN column and using .count() on the Purchase ID column.
- The total purchase per person was calculated by grouping by the SN column and using .sum() on the Price column.
- Both calculations were then passed to variables.
- The average purchase price per player was calculated by diving the total purchase per person by the total purchase count per person, then rounding to 2 decimal points.
- The variables were then passed to a data frame for display output and sorted using .sort_values(), in descending order, by Total Purchase Value. Then, .head(5) was used to display the top 5 spenders. The data frame was formatted using .style.format() to add dollar signs to the rows with columns containing monetary values.

```python
user_purchase_count = df.groupby(["SN"])["Purchase ID"].count()

user_purchase_total = df.groupby(["SN"])["Price"].sum()

user_avg_purchse = round(user_purchase_total / user_purchase_count, 2)

top_spenders = pd.DataFrame({
    "Purchase Count": user_purchase_count,
    "Average Purchase Price": user_avg_purchse,
    "Total Purchase Value": user_purchase_total
})

sorted_spenders = top_spenders.sort_values(by=["Total Purchase Value"], ascending=False).head(5)

sorted_spenders.style.format({"Average Purchase Price": "${:,.2f}", 
                          "Total Purchase Value": "${:,.2f}"})
```

### Most Popular Items 
- To analyze the most popular items, a data frame was created out of the columns Item ID, Item Name, and Price from the original data frame.
- The purchase count was calculated by grouping by the Item ID and Item Name columns and using .count() on the Item ID column.
- The item price was assigned to a variable by grouping by the Item ID and Item Name columns and using .mean() on the Price column.
- The total purchase value was calculated by grouping by the Item ID and Item Name columns and using .sum() on the Price column.
- The calculations were then assigned to variables.
- The variables were then passed to a data frame for display output and sorted using .sort_values(), in descending order, by Purchase Count. To get the top 5 most popular items, .head(5) was used. The data frame was then formatted using .style.format() to add dollar signs to all rows in columns with monetary values.

```python
purchase_df = df[["Item ID", "Item Name", "Price"]]

purchase_count = purchase_df.groupby(["Item ID", "Item Name"])["Item ID"].count()

item_price = purchase_df.groupby(["Item ID", "Item Name"])["Price"].mean()

total_purchase_value = purchase_df.groupby(["Item ID", "Item Name"])["Price"].sum()

popular_items = pd.DataFrame({
    "Purchase Count": purchase_count,
    "Item Price": item_price,
    "Total Purchase Value": total_purchase_value
})

sorted_items = popular_items.sort_values(by=["Purchase Count"], ascending=False).head(5)

sorted_items.style.format({"Item Price": "${:,.2f}", 
                          "Total Purchase Value": "${:,.2f}"})
```

### Most Profitable Items 
- The most profitable items table was created by reusing the Popular Items data frame and sorting by Total Purchase Value in descending order with .head(5). The data frame was then formatted using .style.format() to add dollar signs to all rows in columns with monetary values.
```python
sorted_profit_items = popular_items.sort_values(by=["Total Purchase Value"], ascending=False).head(5)

sorted_profit_items.style.format({"Item Price": "${:,.2f}", 
                          "Total Purchase Value": "${:,.2f}"})
```
