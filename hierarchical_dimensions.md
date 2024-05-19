# Dimension Hierarchies 

## Fixed Depth Positional Hierarchies 
- these are easiest to deal with because they have a fixed depth 
- series of many to one relationships 
- e.g. one department for many products
- e.g.
- Department > Category > Brand > Product
- the levels should appear as separate "positional attributes" in the dimension table. 

as seen in: 
```
Chapter 3 Retail Sales , p 84
Chapter 7 Accounting , p 214
Chapter 19 ETL Subsystems and Techniques , p 470
Chapter 20 ETL System Process and Tasks , p 501
```

## Variable depth hierarchies 

- geographic hierarchies
- range in depth 
- force fit slightly ragged hierarchies into a fixed depth positional design with separate dimension attributes for the maximum level of levels

```
Chapter 7 Accounting , p 214
```


# Chapter 7 - Accounting - Dimension Attribute Hierarchies

- four hierachies: calendar levels, account levels, geographic levels, and organization levels  
- calendar:
    - fixed depth hierarchy
    - e.g. year > fiscal period > day
    - another: year > month > day 
    - the above are two different hierarchies 
    - 


**warning**:
- avoid abstract names for fixed level hierarchies 
- e.g. level1, level2
- cheap way to avoid properly naming ragged hierarchies

# Slightly Ragged Variable Depth Hierarchies

- geographic hierarchies 
- country > state > county > city > district > address
- there is a narrow range of valid levels
    - e.g. 4 to 6
    - if it is more than that, this approach will not work

If some of your data is more detailed than others:
- e.g. for one address you only have (address, city, state, country)
- but for another you have (address, district, city, state, country) 
- then you can repeat the larger positional element various times


```
loc key (PK) | address | district | city | state | country 
1  | 135 birch | ridgewood | NYC | NY | US 
2  | 458 11th  | NYC       | NYC | NY | US 
```


# Ragged Variable Depth Hierarchies 

- trees
- indeterminate length
- e.g. an enterprise with various organizations

Classic way of handling hierarchical data:
- keep a parent key in each row of the dimension table
- so for each row you know what its parent is
- this is a recursive pointer

Better solution:
- build a special bridge table
- it should be independent from the primary dimension table 
- grain: each path in the tree from the parent to all the children below it
- "Map Bridge"
- a row must be constructed for each possible parent to each possible child
- there must also be a row that connects the parent to itself (why?) 

Parent_Org_Key | Child_Org_Key | Depth_From_Parent | Highest_Parent_Flag | Lowest_Child_Flag 

1 | 1 | 0 | TRUE | FALSE 
1 | 2 | 1 | TRUE | FALSE
1 | 3 | 2 | TRUE | TRUE 
1 | 4 | 2 | TRUE | FALSE

- a `Lowest_Child_Flag` value of TRUE indicates a root node in the tree! 
- two rows can have the same depth from parent if they are at the same level in the tree! (e.g. in a binary tree)



