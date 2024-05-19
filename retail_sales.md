# Retail Sales

# Four step Dimensional Design Process

1. Select the Business Process
2. Declare the grain
    - i.e. what will one row in the fact table represent
3. Identify the dimensions
    - how to describe the data resulting from a given business process  
4. Identify the facts
    - you may have several facts related to a single business process
    - if that's the case, then you need to have multiple fact tables
        - actually they only need to be separate tables if they occur over different time periods/processes
        - if they can be obtained from the same process, then they can just be multiple columns  
    - typical facts are additive figures (quantity, cost, sales)



# Grocery store example

- each store has 60,000 products, with a SKU assigned to each one
- POS: point of sales (cash register)
- vendors make deliveries at the back door
- ordering, stocking, and selling products while maximizing profit 
    - max profit: charge as much as possible for each product
    - lower costs for product acquisition and overhead
    - attracting customers 
- pricing and promotions 
- to create a surge in volume of product sold: lower the price 


# Modeling purchases 

- POS system
- retail sales transactions
- "which products are selling in which stores on which days under what promotional conditions in which transactions" 

# grain

- lowest grain: individual product on a POS transaction
- single line item on a receipt

# dimensions

- product
- transaction 
- date (of sale)
- store
- promotion 
- cahsier 
- payment method 
- POS transaction ticket (degenerate dimension)  

# facts  

- fact should be true to the grain
- extended discount dollar amount:
    - sales quantity * the unit discount amount
- standard dollar cost for the product as delivered to the store by the vendor
- 

# Retail Sales Fact (table)  

- Date Key
- Product Key
- Store Key
- Cahsier Key
- Payment Method Key
- POS Transaction # (degenerate dimension)
- Sales Quantity 
    - e.g. how many units sold for the item being purchased
- Regular Unit Price
- Discount Unit Price
- Net Unit Price
    - Regular Unit Price - Discount Unit Price 
- Extended Discount Dollar Amount
    - units sold * unit discount amount 
- Extended Sales Dollar Amount (revenue)
    - units sold * Regular Unit Price
- Extended Cost Dollar Amount
    - units sold * cost from vendor 
- Extended Gross Profit Dollar Amount
    -  extended sales dollar amount -  extended cost dollar amount


* they recommend that we store `calculated derived facts` in the database! 
* you can store it in the same fact table or in a view


# Non Additive Facts  

- percentages and ratios (e.g. gross margin) are non-additive 
- the numerator and denominator should be stored in the fact table 
- the ratios are then computed for a slice of the fact table
- you want to calculate the ratio of the sums, not the sum of the ratios 

- gross margin:
    - profit / revenue 
    - dividing the gross profit by the extended sales dollar revenue
    - e.g. cost was $10, revenue was $15, gross profit (revenue - cost) was $5
        - so $5 / $15 = 0.3

- **unit price** is a non-additive fact!
    - you sold one widget at a unit price of $1.00
    - you then sold 4 widgets at a price of $0.50 each 
    - you can sum the sales quantity --> 5 units sold
    - you can sum the dollar mounts --> $3 total sold 
    - you **cannot** sum the uni prices and say the total unit price was $1.50
    - you **cannot** average them, and say the average unit price $0.75
    - you **can** get the weighted average unit price:
        - total sales amount ($3) / total quantity ($5 units) 
        - ($1 * 1) + ($ 0.5 * 4) / 5 

# Transaction Fact Tables  

