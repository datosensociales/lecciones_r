Tidy Data
================

Dataset 1
---------

    ## # A tibble: 16 x 11
    ##    reltrad `Less than $10,~ `10 to under $2~ `20 to under $3~
    ##    <chr>              <dbl>            <dbl>            <dbl>
    ##  1 Evange~              575              869             1064
    ##  2 Mainli~              289              495              619
    ##  3 Histor~              228              244              236
    ##  4 Cathol~              418              617              732
    ##  5 Mormon                29               40               48
    ##  6 Orthod~               13               17               23
    ##  7 Jehova~               20               27               24
    ##  8 Other ~                9                7               11
    ##  9 Jewish                19               19               25
    ## 10 Muslim                 6                7                9
    ## 11 Buddhi~               27               21               30
    ## 12 Hindu                  1                9                7
    ## 13 Other ~                5                2                3
    ## 14 Other ~               20               33               40
    ## 15 Unaffi~              256              360              471
    ## 16 Don’t ~               15               14               15
    ## # ... with 7 more variables: `30 to under $40,000` <dbl>, `40 to under
    ## #   $50,000` <dbl>, `50 to under $75,000` <dbl>, `75 to under
    ## #   $100,000` <dbl>, `100 to under $150,000` <dbl>, `$150,000 or
    ## #   more` <dbl>, `Don't know/Refused (VOL.)` <dbl>

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

    ## # A tibble: 16 x 11
    ##    reltrad `Less than $10,~ `10 to under $2~ `20 to under $3~
    ##    <chr>              <dbl>            <dbl>            <dbl>
    ##  1 Evange~              575              869             1064
    ##  2 Mainli~              289              495              619
    ##  3 Histor~              228              244              236
    ##  4 Cathol~              418              617              732
    ##  5 Mormon                29               40               48
    ##  6 Orthod~               13               17               23
    ##  7 Jehova~               20               27               24
    ##  8 Other ~                9                7               11
    ##  9 Jewish                19               19               25
    ## 10 Muslim                 6                7                9
    ## 11 Buddhi~               27               21               30
    ## 12 Hindu                  1                9                7
    ## 13 Other ~                5                2                3
    ## 14 Other ~               20               33               40
    ## 15 Unaffi~              256              360              471
    ## 16 Don’t ~               15               14               15
    ## # ... with 7 more variables: `30 to under $40,000` <dbl>, `40 to under
    ## #   $50,000` <dbl>, `50 to under $75,000` <dbl>, `75 to under
    ## #   $100,000` <dbl>, `100 to under $150,000` <dbl>, `$150,000 or
    ## #   more` <dbl>, `Don't know/Refused (VOL.)` <dbl>

Después
-------

    ## # A tibble: 160 x 3
    ##    reltrad                                income             cant
    ##    <chr>                                  <chr>             <dbl>
    ##  1 Evangelical Protestant Churches        Less than $10,000   575
    ##  2 Mainline Protestant Churches           Less than $10,000   289
    ##  3 Historically Black Protestant Churches Less than $10,000   228
    ##  4 Catholic                               Less than $10,000   418
    ##  5 Mormon                                 Less than $10,000    29
    ##  6 Orthodox                               Less than $10,000    13
    ##  7 Jehovah's Witness                      Less than $10,000    20
    ##  8 Other Christian                        Less than $10,000     9
    ##  9 Jewish                                 Less than $10,000    19
    ## 10 Muslim                                 Less than $10,000     6
    ## # ... with 150 more rows

Múltiples variables en una columna
==================================

    ## # A tibble: 49 x 13
    ##    state f1524 f2534 f3544 f4554 f5564 `f6565+` m1524 m2534 m3544 m4554
    ##    <chr> <dbl> <dbl> <dbl> <dbl> <dbl>    <dbl> <dbl> <dbl> <dbl> <dbl>
    ##  1 Alab~    13    38    51    72    82       91    41    40    47    64
    ##  2 Ariz~    22    39    49    50    52       78    20    39    57    43
    ##  3 Arka~    12    24    31    43    47       58    12    20    21    28
    ##  4 Cali~   110   259   337   379   294      385   181   240   324   345
    ##  5 Colo~    21    44    53    56    55       66    23    25    52    61
    ##  6 Conn~    11    23    42    41    34       56    15    17    25    37
    ##  7 Dela~     6    11     7    12    11       16     1     3     5    12
    ##  8 Dist~     2     3     5     8    10        9     2    10     9     9
    ##  9 Flor~    35    83   128   200   173      286    57    78   103   164
    ## 10 Geor~    34    56    99   106   102      110    32    67    92    91
    ## # ... with 39 more rows, and 2 more variables: m5564 <dbl>, `m6565+` <dbl>

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

    ## # A tibble: 49 x 13
    ##    state f1524 f2534 f3544 f4554 f5564 `f6565+` m1524 m2534 m3544 m4554
    ##    <chr> <dbl> <dbl> <dbl> <dbl> <dbl>    <dbl> <dbl> <dbl> <dbl> <dbl>
    ##  1 Alab~    13    38    51    72    82       91    41    40    47    64
    ##  2 Ariz~    22    39    49    50    52       78    20    39    57    43
    ##  3 Arka~    12    24    31    43    47       58    12    20    21    28
    ##  4 Cali~   110   259   337   379   294      385   181   240   324   345
    ##  5 Colo~    21    44    53    56    55       66    23    25    52    61
    ##  6 Conn~    11    23    42    41    34       56    15    17    25    37
    ##  7 Dela~     6    11     7    12    11       16     1     3     5    12
    ##  8 Dist~     2     3     5     8    10        9     2    10     9     9
    ##  9 Flor~    35    83   128   200   173      286    57    78   103   164
    ## 10 Geor~    34    56    99   106   102      110    32    67    92    91
    ## # ... with 39 more rows, and 2 more variables: m5564 <dbl>, `m6565+` <dbl>

Intermedio (gather)
-------------------

    ## # A tibble: 588 x 3
    ##    state                sex_age  cant
    ##    <chr>                <chr>   <dbl>
    ##  1 Alabama              f1524      13
    ##  2 Arizona              f1524      22
    ##  3 Arkansas             f1524      12
    ##  4 California           f1524     110
    ##  5 Colorado             f1524      21
    ##  6 Connecticut          f1524      11
    ##  7 Delaware             f1524       6
    ##  8 District of Columbia f1524       2
    ##  9 Florida              f1524      35
    ## 10 Georgia              f1524      34
    ## # ... with 578 more rows

Después (separate)
------------------

    ## # A tibble: 588 x 4
    ##    state                sex   age_range  cant
    ##    <chr>                <chr> <chr>     <dbl>
    ##  1 Alabama              f     1524         13
    ##  2 Arizona              f     1524         22
    ##  3 Arkansas             f     1524         12
    ##  4 California           f     1524        110
    ##  5 Colorado             f     1524         21
    ##  6 Connecticut          f     1524         11
    ##  7 Delaware             f     1524          6
    ##  8 District of Columbia f     1524          2
    ##  9 Florida              f     1524         35
    ## 10 Georgia              f     1524         34
    ## # ... with 578 more rows

Variables en filas y columnas
=============================

    ## # A tibble: 20 x 17
    ##      row id     year month element d1       d2    d3    d4    d5 d6   
    ##    <dbl> <chr> <dbl> <dbl> <chr>   <lgl> <dbl> <dbl> <dbl> <dbl> <lgl>
    ##  1     1 MX00~  2010     1 TMAX    NA       NA    NA    NA    NA NA   
    ##  2     2 MX00~  2010     1 TMIN    NA       NA    NA    NA    NA NA   
    ##  3     3 MX00~  2010     2 TMAX    NA      273   241    NA    NA NA   
    ##  4     4 MX00~  2010     2 TMIN    NA      144   144    NA    NA NA   
    ##  5     5 MX00~  2010     3 TMAX    NA       NA    NA    NA   321 NA   
    ##  6     6 MX00~  2010     3 TMIN    NA       NA    NA    NA   142 NA   
    ##  7     7 MX00~  2010     4 TMAX    NA       NA    NA    NA    NA NA   
    ##  8     8 MX00~  2010     4 TMIN    NA       NA    NA    NA    NA NA   
    ##  9     9 MX00~  2010     5 TMAX    NA       NA    NA    NA    NA NA   
    ## 10    10 MX00~  2010     5 TMIN    NA       NA    NA    NA    NA NA   
    ## 11    11 MX00~  2010     6 TMAX    NA       NA    NA    NA    NA NA   
    ## 12    12 MX00~  2010     6 TMIN    NA       NA    NA    NA    NA NA   
    ## 13    13 MX00~  2010     7 TMAX    NA       NA   286    NA    NA NA   
    ## 14    14 MX00~  2010     7 TMIN    NA       NA   175    NA    NA NA   
    ## 15    15 MX00~  2010     8 TMAX    NA       NA    NA    NA   296 NA   
    ## 16    16 MX00~  2010     8 TMIN    NA       NA    NA    NA   158 NA   
    ## 17    17 MX00~  2010    10 TMAX    NA       NA    NA    NA   270 NA   
    ## 18    18 MX00~  2010    10 TMIN    NA       NA    NA    NA   140 NA   
    ## 19    19 MX00~  2010    11 TMAX    NA      313    NA   272   263 NA   
    ## 20    20 MX00~  2010    11 TMIN    NA      163    NA   120    79 NA   
    ## # ... with 6 more variables: d7 <dbl>, d8 <dbl>, d9 <lgl>, d10 <dbl>,
    ## #   d11 <dbl>, d12 <lgl>

¿Cuáles son las variables en este dataset?
==========================================

Discutir 1 minuto con une compañere
Pistas:
- TMIN = temperatura mínima
- id = identificador de estación atmosférica

Solución
--------

Para reunir los valores de la variable `day` usamos `gather`.
Y para expandir las variables `tmax` y `tmin` usamos `spread`. Luego, utilizo `mutate` y `str_remove` para eliminar la 'd' en los valores de la variable `day` y `arrange` para ordernar por `year`, `month`, `day` e `id`

``` r
tidy3 <- raw3 %>% 
  gather(key = "day",
         value = "temp", 
         d1:d12) %>% 
  spread(key = element,
         value = temp) %>% 
  mutate(day = as.numeric(str_remove(day, "d"))) %>% 
  arrange(year, month, day, id)
```

Antes
-----

    ## # A tibble: 20 x 17
    ##      row id     year month element d1       d2    d3    d4    d5 d6   
    ##    <dbl> <chr> <dbl> <dbl> <chr>   <lgl> <dbl> <dbl> <dbl> <dbl> <lgl>
    ##  1     1 MX00~  2010     1 TMAX    NA       NA    NA    NA    NA NA   
    ##  2     2 MX00~  2010     1 TMIN    NA       NA    NA    NA    NA NA   
    ##  3     3 MX00~  2010     2 TMAX    NA      273   241    NA    NA NA   
    ##  4     4 MX00~  2010     2 TMIN    NA      144   144    NA    NA NA   
    ##  5     5 MX00~  2010     3 TMAX    NA       NA    NA    NA   321 NA   
    ##  6     6 MX00~  2010     3 TMIN    NA       NA    NA    NA   142 NA   
    ##  7     7 MX00~  2010     4 TMAX    NA       NA    NA    NA    NA NA   
    ##  8     8 MX00~  2010     4 TMIN    NA       NA    NA    NA    NA NA   
    ##  9     9 MX00~  2010     5 TMAX    NA       NA    NA    NA    NA NA   
    ## 10    10 MX00~  2010     5 TMIN    NA       NA    NA    NA    NA NA   
    ## 11    11 MX00~  2010     6 TMAX    NA       NA    NA    NA    NA NA   
    ## 12    12 MX00~  2010     6 TMIN    NA       NA    NA    NA    NA NA   
    ## 13    13 MX00~  2010     7 TMAX    NA       NA   286    NA    NA NA   
    ## 14    14 MX00~  2010     7 TMIN    NA       NA   175    NA    NA NA   
    ## 15    15 MX00~  2010     8 TMAX    NA       NA    NA    NA   296 NA   
    ## 16    16 MX00~  2010     8 TMIN    NA       NA    NA    NA   158 NA   
    ## 17    17 MX00~  2010    10 TMAX    NA       NA    NA    NA   270 NA   
    ## 18    18 MX00~  2010    10 TMIN    NA       NA    NA    NA   140 NA   
    ## 19    19 MX00~  2010    11 TMAX    NA      313    NA   272   263 NA   
    ## 20    20 MX00~  2010    11 TMIN    NA      163    NA   120    79 NA   
    ## # ... with 6 more variables: d7 <dbl>, d8 <dbl>, d9 <lgl>, d10 <dbl>,
    ## #   d11 <dbl>, d12 <lgl>

Intermedio (gather)
-------------------

``` r
raw3 %>% 
  gather(key = "day",
         value = "temp", 
         d1:d12)
```

    ## # A tibble: 240 x 7
    ##      row id           year month element day    temp
    ##    <dbl> <chr>       <dbl> <dbl> <chr>   <chr> <dbl>
    ##  1     1 MX000017004  2010     1 TMAX    d1       NA
    ##  2     2 MX000017004  2010     1 TMIN    d1       NA
    ##  3     3 MX000017004  2010     2 TMAX    d1       NA
    ##  4     4 MX000017004  2010     2 TMIN    d1       NA
    ##  5     5 MX000017004  2010     3 TMAX    d1       NA
    ##  6     6 MX000017004  2010     3 TMIN    d1       NA
    ##  7     7 MX000017004  2010     4 TMAX    d1       NA
    ##  8     8 MX000017004  2010     4 TMIN    d1       NA
    ##  9     9 MX000017004  2010     5 TMAX    d1       NA
    ## 10    10 MX000017004  2010     5 TMIN    d1       NA
    ## # ... with 230 more rows

Después (spread)
----------------

``` r
raw3 %>% 
  gather(key = "day",
         value = "temp", 
         d1:d12) %>% 
  spread(key = element,
         value = temp)
```

    ## # A tibble: 240 x 7
    ##      row id           year month day    TMAX  TMIN
    ##    <dbl> <chr>       <dbl> <dbl> <chr> <dbl> <dbl>
    ##  1     1 MX000017004  2010     1 d1       NA    NA
    ##  2     1 MX000017004  2010     1 d10      NA    NA
    ##  3     1 MX000017004  2010     1 d11      NA    NA
    ##  4     1 MX000017004  2010     1 d12      NA    NA
    ##  5     1 MX000017004  2010     1 d2       NA    NA
    ##  6     1 MX000017004  2010     1 d3       NA    NA
    ##  7     1 MX000017004  2010     1 d4       NA    NA
    ##  8     1 MX000017004  2010     1 d5       NA    NA
    ##  9     1 MX000017004  2010     1 d6       NA    NA
    ## 10     1 MX000017004  2010     1 d7       NA    NA
    ## # ... with 230 more rows

Después II (mutate y arrange)
-----------------------------

    ## # A tibble: 240 x 7
    ##      row id           year month   day  TMAX  TMIN
    ##    <dbl> <chr>       <dbl> <dbl> <dbl> <dbl> <dbl>
    ##  1     1 MX000017004  2010     1     1    NA    NA
    ##  2     2 MX000017004  2010     1     1    NA    NA
    ##  3     1 MX000017004  2010     1     2    NA    NA
    ##  4     2 MX000017004  2010     1     2    NA    NA
    ##  5     1 MX000017004  2010     1     3    NA    NA
    ##  6     2 MX000017004  2010     1     3    NA    NA
    ##  7     1 MX000017004  2010     1     4    NA    NA
    ##  8     2 MX000017004  2010     1     4    NA    NA
    ##  9     1 MX000017004  2010     1     5    NA    NA
    ## 10     2 MX000017004  2010     1     5    NA    NA
    ## # ... with 230 more rows

Múltiples tipos en la misma tabla
=================================

    ## # A tibble: 317 x 83
    ##     year artist.inverted track time  genre date.entered date.peaked
    ##    <dbl> <chr>           <chr> <tim> <chr> <date>       <date>     
    ##  1  2000 Destiny's Child Inde~ 03:38 Rock  2000-09-23   2000-11-18 
    ##  2  2000 Santana         Mari~ 04:18 Rock  2000-02-12   2000-04-08 
    ##  3  2000 Savage Garden   I Kn~ 04:07 Rock  1999-10-23   2000-01-29 
    ##  4  2000 Madonna         Music 03:45 Rock  2000-08-12   2000-09-16 
    ##  5  2000 Aguilera, Chri~ Come~ 03:38 Rock  2000-08-05   2000-10-14 
    ##  6  2000 Janet           Does~ 04:17 Rock  2000-06-17   2000-08-26 
    ##  7  2000 Destiny's Child Say ~ 04:31 Rock  1999-12-25   2000-03-18 
    ##  8  2000 Iglesias, Enri~ Be W~ 03:36 Latin 2000-04-01   2000-06-24 
    ##  9  2000 Sisqo           Inco~ 03:52 Rock  2000-06-24   2000-08-12 
    ## 10  2000 Lonestar        Amaz~ 04:25 Coun~ 1999-06-05   2000-03-04 
    ## # ... with 307 more rows, and 76 more variables: x1st.week <dbl>,
    ## #   x2nd.week <dbl>, x3rd.week <dbl>, x4th.week <dbl>, x5th.week <dbl>,
    ## #   x6th.week <dbl>, x7th.week <dbl>, x8th.week <dbl>, x9th.week <dbl>,
    ## #   x10th.week <dbl>, x11th.week <dbl>, x12th.week <dbl>,
    ## #   x13th.week <dbl>, x14th.week <dbl>, x15th.week <dbl>,
    ## #   x16th.week <dbl>, x17th.week <dbl>, x18th.week <dbl>,
    ## #   x19th.week <dbl>, x20th.week <dbl>, x21st.week <dbl>,
    ## #   x22nd.week <dbl>, x23rd.week <dbl>, x24th.week <dbl>,
    ## #   x25th.week <dbl>, x26th.week <dbl>, x27th.week <dbl>,
    ## #   x28th.week <dbl>, x29th.week <dbl>, x30th.week <dbl>,
    ## #   x31st.week <dbl>, x32nd.week <dbl>, x33rd.week <dbl>,
    ## #   x34th.week <dbl>, x35th.week <dbl>, x36th.week <dbl>,
    ## #   x37th.week <dbl>, x38th.week <dbl>, x39th.week <dbl>,
    ## #   x40th.week <dbl>, x41st.week <dbl>, x42nd.week <dbl>,
    ## #   x43rd.week <dbl>, x44th.week <dbl>, x45th.week <dbl>,
    ## #   x46th.week <dbl>, x47th.week <dbl>, x48th.week <dbl>,
    ## #   x49th.week <dbl>, x50th.week <dbl>, x51st.week <dbl>,
    ## #   x52nd.week <dbl>, x53rd.week <dbl>, x54th.week <dbl>,
    ## #   x55th.week <dbl>, x56th.week <dbl>, x57th.week <dbl>,
    ## #   x58th.week <dbl>, x59th.week <dbl>, x60th.week <dbl>,
    ## #   x61st.week <dbl>, x62nd.week <dbl>, x63rd.week <dbl>,
    ## #   x64th.week <dbl>, x65th.week <dbl>, x66th.week <lgl>,
    ## #   x67th.week <lgl>, x68th.week <lgl>, x69th.week <lgl>,
    ## #   x70th.week <lgl>, x71st.week <lgl>, x72nd.week <lgl>,
    ## #   x73rd.week <lgl>, x74th.week <lgl>, x75th.week <lgl>, x76th.week <lgl>

Primera limpieza
----------------

``` r
raw4 %>% 
  gather(semana, rank, x1st.week:x76th.week) %>% 
  mutate(semana = as.numeric(str_extract(semana, "[0-9]+"))) %>% 
  arrange(track, semana)
```

    ## # A tibble: 24,092 x 9
    ##     year artist.inverted track time  genre date.entered date.peaked semana
    ##    <dbl> <chr>           <chr> <tim> <chr> <date>       <date>       <dbl>
    ##  1  2000 Nelly           (Hot~ 04:17 Rap   2000-04-29   2000-09-16       1
    ##  2  2000 Nelly           (Hot~ 04:17 Rap   2000-04-29   2000-09-16       2
    ##  3  2000 Nelly           (Hot~ 04:17 Rap   2000-04-29   2000-09-16       3
    ##  4  2000 Nelly           (Hot~ 04:17 Rap   2000-04-29   2000-09-16       4
    ##  5  2000 Nelly           (Hot~ 04:17 Rap   2000-04-29   2000-09-16       5
    ##  6  2000 Nelly           (Hot~ 04:17 Rap   2000-04-29   2000-09-16       6
    ##  7  2000 Nelly           (Hot~ 04:17 Rap   2000-04-29   2000-09-16       7
    ##  8  2000 Nelly           (Hot~ 04:17 Rap   2000-04-29   2000-09-16       8
    ##  9  2000 Nelly           (Hot~ 04:17 Rap   2000-04-29   2000-09-16       9
    ## 10  2000 Nelly           (Hot~ 04:17 Rap   2000-04-29   2000-09-16      10
    ## # ... with 24,082 more rows, and 1 more variable: rank <dbl>

¿Cuál es mi unidad de observación en esta tabla?
================================================

¿Es la canción? ¿Es canción-semana?
¿Cuántas unidades de observación hay? Discutan con un compañere durante un minuto

Normalización
-------------

Cada hecho sobre una canción se repite muchas veces. Señal que muchos tipos de unidades experimentales están en la misma tabla. Podemos guardar nuestros datos más eficientemente separándolos en distintas tablas para cada tipo de unidad.

Necesitamos dividir la tabla en dos: una tabla "canción" y una tabla "ranking"

Tabla 1: canción
----------------

    ## # A tibble: 317 x 7
    ##     year artist.inverted  track        time  genre date.entered date.peaked
    ##    <dbl> <chr>            <chr>        <tim> <chr> <date>       <date>     
    ##  1  2000 Destiny's Child  Independent~ 03:38 Rock  2000-09-23   2000-11-18 
    ##  2  2000 Santana          Maria, Maria 04:18 Rock  2000-02-12   2000-04-08 
    ##  3  2000 Savage Garden    I Knew I Lo~ 04:07 Rock  1999-10-23   2000-01-29 
    ##  4  2000 Madonna          Music        03:45 Rock  2000-08-12   2000-09-16 
    ##  5  2000 Aguilera, Chris~ Come On Ove~ 03:38 Rock  2000-08-05   2000-10-14 
    ##  6  2000 Janet            Doesn't Rea~ 04:17 Rock  2000-06-17   2000-08-26 
    ##  7  2000 Destiny's Child  Say My Name  04:31 Rock  1999-12-25   2000-03-18 
    ##  8  2000 Iglesias, Enriq~ Be With You  03:36 Latin 2000-04-01   2000-06-24 
    ##  9  2000 Sisqo            Incomplete   03:52 Rock  2000-06-24   2000-08-12 
    ## 10  2000 Lonestar         Amazed       04:25 Coun~ 1999-06-05   2000-03-04 
    ## # ... with 307 more rows

Tabla2: ranking
---------------

    ## # A tibble: 5,307 x 3
    ##    track                      semana  rank
    ##    <chr>                       <dbl> <dbl>
    ##  1 (Hot S**t) Country Grammar      1   100
    ##  2 (Hot S**t) Country Grammar      2    99
    ##  3 (Hot S**t) Country Grammar      3    96
    ##  4 (Hot S**t) Country Grammar      4    76
    ##  5 (Hot S**t) Country Grammar      5    55
    ##  6 (Hot S**t) Country Grammar      6    37
    ##  7 (Hot S**t) Country Grammar      7    24
    ##  8 (Hot S**t) Country Grammar      8    24
    ##  9 (Hot S**t) Country Grammar      9    30
    ## 10 (Hot S**t) Country Grammar     10    36
    ## # ... with 5,297 more rows
