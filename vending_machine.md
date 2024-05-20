# Vending Machine


grain: line item on a receipt 

Fact Table:
- date key
- transaction_id
    - degenerate dimension (no dimension table)
- product id
- location id 
- units_sold
- unit_price
- revenue 
    - units_sold * unit_price
- unit_cost
    - i.e. how much did the vendor buy it for
- extended_cost
    - units_sold * unit_cost
- profit
    - revenue - extended_cost


Location Table:
location_id | capacity | cur_capacity
A1          |  5       | 0
A2          |  5       | 1
A3          |  5       | 0


product table:
product_id | name | brand | unit_price 
1            oreos  oreos   1.00
2            yogurt fayeh   3.00


Product to Location Table:
location_id | product_id 
A1          | 1
A2          | 2


query: can the customer purchase something...
- e.g. 2 oreos and 1 yogurt

try_to_purchase(dollar_amount, location, quantity) -> float (remaining dollar amount)
$10, A1, 1
- if they say A1, we get the product at A1
    - take input quanity * unit_price = $2
    - that is less than $10, so we're good
    - decrease remaining_dollar_amount to $2
- if cur_capacity is at 5, then no item available
    - cur_capacity is at < 5 so we're good
    - decrease cur_capacity to 4
