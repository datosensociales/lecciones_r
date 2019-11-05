Tidy Data
================

Dataset 1
---------

| reltrad                                |  Less than $10,000|  10 to under $20,000|  20 to under $30,000|  30 to under $40,000|  40 to under $50,000|  50 to under $75,000|  75 to under $100,000|  100 to under $150,000|  $150,000 or more|
|:---------------------------------------|------------------:|--------------------:|--------------------:|--------------------:|--------------------:|--------------------:|---------------------:|----------------------:|-----------------:|
| Evangelical Protestant Churches        |                575|                  869|                 1064|                  982|                  881|                 1486|                   949|                    723|               414|
| Mainline Protestant Churches           |                289|                  495|                  619|                  655|                  651|                 1107|                   939|                    753|               634|
| Historically Black Protestant Churches |                228|                  244|                  236|                  238|                  197|                  223|                   131|                     81|                78|
| Catholic                               |                418|                  617|                  732|                  670|                  638|                 1116|                   949|                    792|               633|
| Mormon                                 |                 29|                   40|                   48|                   51|                   56|                  112|                    85|                     49|                42|
| Orthodox                               |                 13|                   17|                   23|                   32|                   32|                   47|                    38|                     42|                46|

¿Cuáles son las variables en este dataset?
==========================================

Discutir con un compañero durante un minuto

La solución
-----------

Arreglar este problema es fácil. Usamos `gather`, de `tidyr` con tres argumentos:

-   El dataset
-   El nombre de la nueva variable `key`
-   El nombre de la nueva variable `value`

``` r
tidy <- gather(data = raw, 
               key = income, 
               value = cant, 
               -reltrad)
```

Antes
-----

| reltrad                                |  Less than $10,000|  10 to under $20,000|  20 to under $30,000|  30 to under $40,000|  40 to under $50,000|  50 to under $75,000|  75 to under $100,000|  100 to under $150,000|  $150,000 or more|
|:---------------------------------------|------------------:|--------------------:|--------------------:|--------------------:|--------------------:|--------------------:|---------------------:|----------------------:|-----------------:|
| Evangelical Protestant Churches        |                575|                  869|                 1064|                  982|                  881|                 1486|                   949|                    723|               414|
| Mainline Protestant Churches           |                289|                  495|                  619|                  655|                  651|                 1107|                   939|                    753|               634|
| Historically Black Protestant Churches |                228|                  244|                  236|                  238|                  197|                  223|                   131|                     81|                78|
| Catholic                               |                418|                  617|                  732|                  670|                  638|                 1116|                   949|                    792|               633|
| Mormon                                 |                 29|                   40|                   48|                   51|                   56|                  112|                    85|                     49|                42|
| Orthodox                               |                 13|                   17|                   23|                   32|                   32|                   47|                    38|                     42|                46|
| Jehovah's Witness                      |                 20|                   27|                   24|                   24|                   21|                   30|                    15|                     11|                 6|
| Other Christian                        |                  9|                    7|                   11|                   13|                   13|                   14|                    18|                     14|                12|
| Jewish                                 |                 19|                   19|                   25|                   25|                   30|                   95|                    69|                     87|               151|
| Muslim                                 |                  6|                    7|                    9|                   10|                    9|                   23|                    16|                      8|                 6|

Después
-------

| reltrad                                | income            |  cant|
|:---------------------------------------|:------------------|-----:|
| Evangelical Protestant Churches        | Less than $10,000 |   575|
| Mainline Protestant Churches           | Less than $10,000 |   289|
| Historically Black Protestant Churches | Less than $10,000 |   228|
| Catholic                               | Less than $10,000 |   418|
| Mormon                                 | Less than $10,000 |    29|
| Orthodox                               | Less than $10,000 |    13|
| Jehovah's Witness                      | Less than $10,000 |    20|
| Other Christian                        | Less than $10,000 |     9|
| Jewish                                 | Less than $10,000 |    19|
| Muslim                                 | Less than $10,000 |     6|

Múltiples variables en una columna
==================================

| state                |  f1524|  f2534|  f3544|  f4554|  f5564|  f6565+|  m1524|  m2534|  m3544|
|:---------------------|------:|------:|------:|------:|------:|-------:|------:|------:|------:|
| Alabama              |     13|     38|     51|     72|     82|      91|     41|     40|     47|
| Arizona              |     22|     39|     49|     50|     52|      78|     20|     39|     57|
| Arkansas             |     12|     24|     31|     43|     47|      58|     12|     20|     21|
| California           |    110|    259|    337|    379|    294|     385|    181|    240|    324|
| Colorado             |     21|     44|     53|     56|     55|      66|     23|     25|     52|
| Connecticut          |     11|     23|     42|     41|     34|      56|     15|     17|     25|
| Delaware             |      6|     11|      7|     12|     11|      16|      1|      3|      5|
| District of Columbia |      2|      3|      5|      8|     10|       9|      2|     10|      9|
| Florida              |     35|     83|    128|    200|    173|     286|     57|     78|    103|
| Georgia              |     34|     56|     99|    106|    102|     110|     32|     67|     92|

¿Cuáles son las variables en este dataset?
==========================================

Discutir con un compañero durante un minuto
Pista: f = female, 1524 = 15 a 24

La solución
-----------

Volvemos a usar `gather` y ahora también vamos a necesitar `separate`

``` r
tidy2 <- raw2 %>% 
  gather(key = sex_age, value = cant, -state) %>% 
  separate(col = sex_age, into = c("sex", "age_range"), sep = 1)
```

Antes
-----

| state                |  f1524|  f2534|  f3544|  f4554|  f5564|  f6565+|  m1524|  m2534|  m3544|
|:---------------------|------:|------:|------:|------:|------:|-------:|------:|------:|------:|
| Alabama              |     13|     38|     51|     72|     82|      91|     41|     40|     47|
| Arizona              |     22|     39|     49|     50|     52|      78|     20|     39|     57|
| Arkansas             |     12|     24|     31|     43|     47|      58|     12|     20|     21|
| California           |    110|    259|    337|    379|    294|     385|    181|    240|    324|
| Colorado             |     21|     44|     53|     56|     55|      66|     23|     25|     52|
| Connecticut          |     11|     23|     42|     41|     34|      56|     15|     17|     25|
| Delaware             |      6|     11|      7|     12|     11|      16|      1|      3|      5|
| District of Columbia |      2|      3|      5|      8|     10|       9|      2|     10|      9|
| Florida              |     35|     83|    128|    200|    173|     286|     57|     78|    103|
| Georgia              |     34|     56|     99|    106|    102|     110|     32|     67|     92|

Intermedio (gather)
-------------------

| state                | sex\_age |  cant|
|:---------------------|:---------|-----:|
| Alabama              | f1524    |    13|
| Arizona              | f1524    |    22|
| Arkansas             | f1524    |    12|
| California           | f1524    |   110|
| Colorado             | f1524    |    21|
| Connecticut          | f1524    |    11|
| Delaware             | f1524    |     6|
| District of Columbia | f1524    |     2|
| Florida              | f1524    |    35|
| Georgia              | f1524    |    34|

Después (separate)
------------------

| state                | sex | age\_range |  cant|
|:---------------------|:----|:-----------|-----:|
| Alabama              | f   | 1524       |    13|
| Arizona              | f   | 1524       |    22|
| Arkansas             | f   | 1524       |    12|
| California           | f   | 1524       |   110|
| Colorado             | f   | 1524       |    21|
| Connecticut          | f   | 1524       |    11|
| Delaware             | f   | 1524       |     6|
| District of Columbia | f   | 1524       |     2|
| Florida              | f   | 1524       |    35|
| Georgia              | f   | 1524       |    34|
