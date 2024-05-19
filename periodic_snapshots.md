# Periodic Snapshot tables 

- events occurring over a period of time 
- e.g. day week or month
- the grain is the period, not the individual transaction  
- even if no activity occurs in the period, a row is still inserted into the table with a 0 or null for each fact   

These can be seen in:
- Chapter 4 -- Inventory
- Chapter 7 -- Accounting
- Chapter 9 -- HR management
- Chapter 10 -- Financial Services  
- Chapter 19 -- ETL subsystems and techniques 


# Accumulating Snapshot Fact Tables 

- a single row summarizes the measurement events occurring at predictable steps between the beginning and the end of a process. 
- e.g. order fulfillment 
- there is a date foreign key for each critical milestone within the process
- you keep coming back and updating the row when those events are completed

