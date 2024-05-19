Other data modeling video:
- https://www.youtube.com/watch?v=gG7upg6QaBI  

Data modeling at the companies he has worked at:
- https://www.youtube.com/watch?v=rqLbn1PQPKA  

Zach Wilson has a Data Modeling video:
- ...



Handling Historical Data:
- fact data itself is already historical
- each event comes in a becomes a row  

Adding new data to a fact table:
- append everything onto the fact table
- sometimes, you replace a row with the same id 
- those two methods will determine how you use the data downstream 

Data history  matters when for example you have a customer dimension, and the customer then moves to another city.
- you could just replace the value in the table
- but you may need to keep track of where they lived previously
- if you need the history then you need to use SCD2.  

https://youtu.be/rqLbn1PQPKA?t=333  

Type 2 or Type 6 are typically implemented.  

# snapshot approach 

- resave the data every day as a new table?
- these are "partitions"

```sql
select * from employee
```

- you have a macro that concatenates all of the snapshot tables 

```sql
select * from employee
where ds = <CURRENT_DS>
```
