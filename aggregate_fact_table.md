# Aggregate Fact Tables

- these are also called OLAP cubes
- built to accelerate query performance

`aggregate navigation`: 
- having atomic fact tables and aggregate fact tables available to the BI layer, so the right table can be chosen at query time

OLAP cubes are meant to be consumed directly by end users.  

Found in chapters:

```
Chapter 15 - E commerce
Chapter 19 - ETL Subsystems 
Chapter 20 - ETL system process 
```


- basic idea is to take a finer grain fact table and aggregate it and create a new fact table over a longer time period.
- e.g. take click stream data and aggregate it to total page visits per month


