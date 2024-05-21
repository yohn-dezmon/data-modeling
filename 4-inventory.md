# Inventory 


**value chain**:
- logical flow of businesses primary activities 
- issue purchase order to manufacturer
    - receive warehouse deliveries
        - warehouse product inventory
            - receive store deliveries
                - store product inventory
                    - retail sales 


**snapshots** at each step of the value chain!  
- each process spawns one or more fact tables  


# Inventory models

1. `periodic snapshot`
- product inventory levels are measured at regular intervals
- placed as separate rows in a fact table

# Inventory Periodic Snapshot

- business process: periodic snapshotting of retail store inventory 
- daily inventory for each product in each store
- dimensions: date, product, store  
- promotions not typically associated with inventory 
    - they are associated with transactions 
- fact `quantity on hand`

Fact Table (Store Inventory Snapshot):
- Date Key
- Product Key
- Store Key 
- Quantity on Hand

This results in dense fact tables, because you have to create rows daily for each product, in each store.  

# reduce snapshot frequency over time
- save on storage
- keep daily snapshots up to 60 days in the past 
- at that point, 

2024-03-21 --> 60 days ago
2024-05-21 --> today 

ok so we have daily data from 3/21 -> 5/21.

How do we aggregate the older data though?
- I guess since you have 3/21 to 4/21
- you could take weekly sums per product per store and store them in an aggregate/historical fact table
- then after each week, since the data


Process:  
- at the end of each week, run a script that would generate new rows in the aggregate week fact table
    - this shows `quantity on hand` of each product for each store for that week
- after that portion of the script runs
    - run a delete script that deletes that week of daily data from the daily fact table
        - you can delete all data with the date range 3/21 -> 3/28

^ The order here matters! 


# Inventory Levels: Semi-additive Facts (!!!)

https://www.youtube.com/watch?v=uH163go3pvQ

- inventory levels are not additive across dates
- they represent snapshots of a level or balance at one point in time 
- they are additive across some dimensions 

Example with checking account:  
- on Mon, balance: $50
- on Tues, same. balance: $50
- on Wed, deposit: $50. balance: $100
- on Friday, you can't sum daily balance's to get $400 ($50 + $50 + $100 + $100 + $100)
- How to combine semi-additive (e.g. account balance, inventory levels)?
    - average them!
    - in this case $400 / 5 = $80 average balance  


How to get average for:  
    - each product for each store over a week?
    - don't use `AVG()` because it will divide by the total number of rows returned from the query
    - you instead have ot use the number of days as the denominator

```sql
SELECT 
    EXTRACT(YEAR FROM date) AS year,
    EXTRACT(WEEK FROM date) AS week,
    product, 
    store, 
    AVG(quantity) AS avg_quantity_per_week
FROM 
    table
GROUP BY 
    EXTRACT(YEAR FROM date), 
    EXTRACT(WEEK FROM date),
    product, 
    store;
```

**if you want to include the starting date of the week, use `date_trunc`**:
```sql
select
    DATE_TRUNC('week', date) as week_start_date,
    product,
    store,
    AVG(quantity) as avg_quantity_per_week
FROM 
    table
GROUP BY 
    DATE_TRUNC('week', date),
    product,
    store;
```
