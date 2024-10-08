# Homework 2 Solution

## 1.1     

π<sub>A,B</sub>(T1)

|A | B |
|---|---|
|1 | x |
|2 | y |
|2 | z |


## 1.2

T1 × π<sub>A</sub>(T1)

|(A) | B | C |  (A)|
|---|---|---| ---|
|1 | x | a | 1 |
|2 | y | c | 1 |
|2 | y | b | 1 |
|2 | z | c | 1 |
|1 | x | a | 2 |
|2 | y | c | 2 |
|2 | y | b | 2 |
|2 | z | c | 2 |

## 1.3

T1 ⨝<sub>T1.B=T2.C</sub> T2

|A | (B) | (C) | (B) | (C) | D |
|---|---|---|---|---|---|
|1 | x | a | 1 | x | c |
|1 | x | a | 3 | x | a |
|2 | y | c | 2 | y | c |
|2 | y | b | 2 | y | c |

## 1.4

(T1 ∪ T2) − (T1 ∩ T2)

|A | B | C |
|---|---|---|
|1 | x | c |
|1 | x | a |
|3 | x | a |
|2 | y | b |
|2 | z | c |

## 1.5

T1 ⨝<sub>T1.A&gt;T2.B</sub> (σ<sub>B&ne;2</sub>(T2))

|A | (B) | (C) | (B) | (C) | D |
|--|-----|---|-----|---|---|
|2 | y   | c | 1   | x | c |
|2 | y   | b | 1   | x | c |
|2 | z   | c | 1   | x | c |


## 1.6

T1 ⨝<sub>T1.A&gt;R.A</sub> p(R(1->A, 2->D), π<sub>B, C</sub>(T2))

| (A) | B | C | (A) | D |
|-----|---|---|-----|---|
|  1  | x | a |  1  | x |
|  2  | y | c |  2  | y |
|  2  | y | b |  2  | y |
|  2  | z | c |  2  | y |

IMPORTANT: You should use the bracket `(<column_name>)` notation or the `<table_name>.<column_name>` *only* for columns with duplicate names! 

In other words, if you bracket every column, or if you put a `<table_name>.` prefix in front of every column, then it's incorrect.

## 2.1 

π<sub>ssn</sub>(π<sub>ssn, companyid</sub>(Person) - π<sub>ssn, companyid</sub>(Holding))

## 2.2 

p(H, π<sub>ssn, companyid, managerid, sharenum</sub>(Holding ⨝<sub>ssn = employeeid</sub>Supervision))

p(Unqualify, π<sub>H.ssn, H.companyid</sub>(σ<sub> H.sharenum &le; Holding.sharenum</sub>(H ⨝<sub>H.managerid = Holding.ssn</sub>Holding)))

π<sub>ssn</sub>(π<sub>ssn, Holding.companyid</sub>(Person ⨝<sub>Person.ssn = Holding.ssn</sub>Holding)- Unqualify)

## 2.3

p(tmp1, Holding)

p(tmp2, Holding)

p(tmp(ssn, s1, s2, s3), π <sub>Holding.ssn, Holding.sharenum, tmp1.sharenum, tmp2.sharenum</sub>(σ<sub>Holding.companyid ≠ tmp1.companyid ∧ Holding.companyid  ≠ tmp2.companyid ∧ tmp2.companyid≠ tmp1.companyid</sub>(Holding ⨝<sub>ssn</sub> tmp1 ⨝<sub>ssn</sub> tmp2)))

π <sub>ssn</sub>(σ<sub>(s1 > s2 + s3) ∨ (s2 > s1 + s3) ∨ (s3 > s1 + s2)</sub>(tmp))


## 3.1 

description: Find the good names that are sold at a price less than their cost from one of their suppliers.

```sql
select distinct g_name 
from Goods, Supply
where Goods.gid = Supply.gid
and price < cost
```

## 3.2 

description: Find the supplier ids of the stores which supply all the goods supplied by supplier "1096".

```sql
select distinct supplyid
from Supply
where not exists(
    select * from Supply as S1
    where S1.supplyid = "1096"
    and not exists(
        select * from Supply as S2 
        where S2.storeid = Store.storeid and 
        S2.g_id = S1.g_id
    )
)
```

## 3.3
description: Find the supplier ids which supply two goods that are sold with the same price.

```sql
select distinct T1.supplyid
from
(
    select supplyid, G1.gid, price
    from Goods as G1, Supply as S1
    where G1.gid = S1.gid
) T1, 
(
    select supplyid, G1.gid, price
    from Goods as G1, Supply as S1
    where G1.gid = S1.gid
) T2
where T1.gid != T2.gid
and T1.price = T2.price
and T1.supplyid = T2.supplyid
```



## 4.1
Find the total price of goods if all supplies are sold.
```sql
select sum(price)
from Goods, Supply
where Goods.gid = Supply.gid
```


## 4.2
Create a table *Supcount* by finding the total number of suppliers providing each good.

```sql
create table Supcount as
(
    select gid, count(supplyid) as c
    from Supply
    group by gid
)
```

## 4.3
Use only the *Supcount* table you created and the Goods table to compute the total price of goods if all suppliers are sold.

```sql
select sum(c*price)
from Goods, Supcount
where Goods.gid = Supcount.gid
```
