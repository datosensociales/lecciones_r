Clase 4
================
Manuel Zapico y Sofia Santamarina
August 29, 2019

# Paquetes dplyr y tidyr

Hoy presentamos dos paquetes de R que facilitan la limpieza y
manipulacion de datos: **dplyr** y **tidyr**.

Primero traemos el paquete que vamos a usar desde nuestra *library*

``` r
library(tidyverse)
```

En este trabajo, vamos a usar una *base de datos* del sitio Gapminder.

<https://www.gapminder.org/>

La base de datos llamada **base\_exp** que vamos compara el PBI per
capita y la expectativa de vida (o **esperanza de vida**). Los datos son
los siguientes:

``` 
  Pais
  Year
  Expectativa de vida
  Poblacion
  PBI_PC
```

Pero tambien vamos a querer saber a que continente pertenece cada pais.
Por eso, necesitamos la base llamada **continente**.

Primero cargamos los datasets. (Tranqui\! Al final de esta leccion vamos
a ver como hacer esto)

``` r
base_exp <- read_csv("Clase_4_files/base_exp.csv")
continente <- read_csv("Clase_4_files/continente.csv")
```

¿Cómo podemos ver este dataset? Para empezar a ver algo, podemos pedir
que nos de un
    resumen

``` r
summary(base_exp)
```

    ##      pais                year         expVida           pobl          
    ##  Length:1704        Min.   :1952   Min.   :23.60   Min.   :6.001e+04  
    ##  Class :character   1st Qu.:1966   1st Qu.:48.20   1st Qu.:2.794e+06  
    ##  Mode  :character   Median :1980   Median :60.71   Median :7.024e+06  
    ##                     Mean   :1980   Mean   :59.47   Mean   :2.960e+07  
    ##                     3rd Qu.:1993   3rd Qu.:70.85   3rd Qu.:1.959e+07  
    ##                     Max.   :2007   Max.   :82.60   Max.   :1.319e+09  
    ##      PBI_PC        
    ##  Min.   :   241.2  
    ##  1st Qu.:  1202.1  
    ##  Median :  3531.8  
    ##  Mean   :  7215.3  
    ##  3rd Qu.:  9325.5  
    ##  Max.   :113523.1

### Uniendo las bases = join

Antes de empezar, queremos unificar la Base con la esperanza de vida y
la de los continentes. Para eso usamos **join**. ?Que variable usamos
para unir? La que compartan las dos bases de datos: *pais*.

``` r
gapminder <- left_join(base_exp, continente)

head(gapminder)
```

    ## # A tibble: 6 x 6
    ##   pais         year expVida     pobl PBI_PC continente
    ##   <chr>       <dbl>   <dbl>    <dbl>  <dbl> <chr>     
    ## 1 Afghanistan  1952    28.8  8425333   779. Asia      
    ## 2 Afghanistan  1957    30.3  9240934   821. Asia      
    ## 3 Afghanistan  1962    32.0 10267083   853. Asia      
    ## 4 Afghanistan  1967    34.0 11537966   836. Asia      
    ## 5 Afghanistan  1972    36.1 13079460   740. Asia      
    ## 6 Afghanistan  1977    38.4 14880372   786. Asia

Listo\! Ya podemos empezar a pulir los datos.

## Las funciones de tidyverse

Ahora vamos a ver las funciones de *tidyverse* que podemos usar para
manejar nuestros datos. Las principales son las siguientes:

``` 
  select
  filter
  mutate
  group_by
  summarize
  arrange
```

## Seleccionar columnas = select

La primera funcion es **select**. Con ella, lo que vamos a hacer es
elegir **columnas**.

Por ejemplo, queremos ver solamente el cambio de *poblacion* para cada
*pais* segun los *años*.

Aplicamos la funcion pero no la asignamos a nada. Queremos tener una
nueva base con esa seleccion, por eso, creamos un nuevo dataframe:

``` r
pais_pob <- select(gapminder, pais, year, pobl)
```

Podemos ver que en el *Enviroment* el dataframe **pais\_pob** tiene tres
variables en lugar de las seis originales.

## Filtrar filas = filter

A continuacion vamos a usar **filter**. Esta funcion sirve para elegir
filas a partir de determinada condicion. Despues, veremos que podemos
ser mas especificos.

### Filtramos datos

Busquemos los datos de
Argentina.

``` r
#Armamos un dataframe llamado "Argentina". Escribimos la funcion "filter", luego la base de datos de origen, la columna que contiene el dato que queremos -"pais"- y el nombre entre comillas. El pedido de la columna es con doble igual (==). Ahora veremos por que. 

argentina <- filter(gapminder, pais == "Argentina")

#¿y America? Si ponemos "America", no va a pasar nada. Porque en el dataset se llama "Americas". Tiene que ser exacto el pedido y siempre entre comillas.

america <- filter(gapminder, continente == "Americas")
```

Ya tenemos dos nuveas bases: una con datos de Argentina y otra con datos
de America. Pero, si quiero elegir por ejemplo de que manera cambio la
poblacion en America despues de 1990?

### Funciones logicas de filter

Para llevar a cabo comparaciones o filtrar a partir de atributo mas
especificos, podemos usar los siguientes valores:

    == igual a 
    != distinto a
    > mayor que 
    >= mayor igual que
    < menor que
    <= menor igual que
    & y
    | o

**NOTA\!**: es comun equivocar el “==” con el “=”. El “=” es utilizado
para asignar. Por ejemplo **pais=“Argentina”** significa asignar el
valor *Argentina* en la variable *pais*. En cambio, si quiero que me
devuelva el valor de pais que ya sea igual a Argentina, tenemos que usar
“==”.

Volvamos a nuestro pedido. Queremos filtrar la poblacion de America
despues de 1990. Simplemente hacemos lo siguiente:

``` r
argentina_90 <- filter(gapminder, pais == "Argentina", year >= 1990)
```

FACIL\!

Quiero los paises con mas de 100 millones de habitantes:

``` r
mas_habitantes <- filter(gapminder, pobl > 100000000)
```

Mas de 100 millones de personas de Asia **o** America.

``` r
am_as_poblados <- filter(gapminder, 
                         continente == "Americas" | continente =="Asia", 
                         pobl > 100000000)
```

De esos dos continentes que tienen 100 millones de personas desde antes
de 1980

``` r
am_as_pob_1980 <- filter(gapminder, 
                         continente == "Americas" | continente =="Asia", 
                         year <= 1980, pobl > 100000000)
```

Pasame todos los paises menos Estados Unidos

``` r
menos_eeuu <- filter(gapminder, pais != "United States")
```

Último\! Paises que antes de 1970 tenian un expectativa de vida mayor a
73 años, y que no sea Estados
Unidos

``` r
exp_vida_1950 <- filter(gapminder, pais != "United States", year <= 1970, expVida > 73)
```

## Pipe %\>%

Ya vimos dos funciones, por lo que podemos ver el **pipe**\! Esto
simplifica nuestra vida. En lugar de tener que hacer funciones anidadas,
solo tenemos que poner SHIFT+CTRL+M. Esto genera el simbolo **%\>%**,
que permite unir las funciones que vamos a pedir. Se llama “pipe”,
literalmente significa “tubo”. Es como decir “despues esto”: select %\>%
filter, seria “select y despues filer”

Por ejemplo, seleccionamos las columnas pais, poblacion y a?o **y
despues** filtramos años mas de 2000 para poblacion de menos de 10
millones.

``` r
#Cada funcion lo hacemos en un nuevo "renglon" para facilitar la lectura.

para_pipe <- select(gapminder, pais, pobl, year) %>% 
    filter(year > 1990, pobl <10000000)
head(para_pipe)
```

    ## # A tibble: 6 x 3
    ##   pais       pobl  year
    ##   <chr>     <dbl> <dbl>
    ## 1 Albania 3326498  1992
    ## 2 Albania 3428038  1997
    ## 3 Albania 3508512  2002
    ## 4 Albania 3600523  2007
    ## 5 Angola  8735988  1992
    ## 6 Angola  9875024  1997

Tambien, para simplificar mas, podemos poner el dataframe y el pipe para
despues hacer las funciones.

``` r
para_pipe <- gapminder %>% 
                      select(pais, pobl, year) %>% 
                      filter(year > 1990, pobl <10000000)

head(para_pipe)
```

    ## # A tibble: 6 x 3
    ##   pais       pobl  year
    ##   <chr>     <dbl> <dbl>
    ## 1 Albania 3326498  1992
    ## 2 Albania 3428038  1997
    ## 3 Albania 3508512  2002
    ## 4 Albania 3600523  2007
    ## 5 Angola  8735988  1992
    ## 6 Angola  9875024  1997

## Agregar nueva columna con cambios de datos = mutate

Con mutate creamos una nueva columna con datos nuevos o utilizando
algunos de los datos que ya tenemos en la base de datos.

Por ejemplo, quiero conocer el PBI de un pais. Tenemos el **PBI per
capita** y la cantidad de poblacion. Por eso, tenemos que multiplicar
ambos datos para conocer cual es el **PBI TOTAL**

``` r
pbi_total <- mutate(gapminder, PBI_TOTAL = pobl*PBI_PC)

head(pbi_total)
```

    ## # A tibble: 6 x 7
    ##   pais         year expVida     pobl PBI_PC continente    PBI_TOTAL
    ##   <chr>       <dbl>   <dbl>    <dbl>  <dbl> <chr>             <dbl>
    ## 1 Afghanistan  1952    28.8  8425333   779. Asia        6567086330.
    ## 2 Afghanistan  1957    30.3  9240934   821. Asia        7585448670.
    ## 3 Afghanistan  1962    32.0 10267083   853. Asia        8758855797.
    ## 4 Afghanistan  1967    34.0 11537966   836. Asia        9648014150.
    ## 5 Afghanistan  1972    36.1 13079460   740. Asia        9678553274.
    ## 6 Afghanistan  1977    38.4 14880372   786. Asia       11697659231.

## Agrupar y combinar datos

Tambien podemos obtener *resumenes* del dataset. Para eso usamos
**summarise**.

Por ejemplo, quiero conocer el promedio de vida de todos los datos del
dataset.

``` r
summarise(gapminder, mean(expVida))
```

    ## # A tibble: 1 x 1
    ##   `mean(expVida)`
    ##             <dbl>
    ## 1            59.5

La expectativa de vida, como podemos ver, es casi 60 años. Pero lo mejor
del **summarise** es poder combinarlo. Por ejemplo, queremos el promedio
expectativa de vida segun pais.

``` r
media_vida_pais <- gapminder %>% 
    group_by(pais) %>% 
    summarise(mean(expVida))
media_vida_pais
```

    ## # A tibble: 142 x 2
    ##    pais        `mean(expVida)`
    ##    <chr>                 <dbl>
    ##  1 Afghanistan            37.5
    ##  2 Albania                68.4
    ##  3 Algeria                59.0
    ##  4 Angola                 37.9
    ##  5 Argentina              69.1
    ##  6 Australia              74.7
    ##  7 Austria                73.1
    ##  8 Bahrain                65.6
    ##  9 Bangladesh             49.8
    ## 10 Belgium                73.6
    ## # ... with 132 more rows

¿Y el valor máximo de **Esperanza de vida** que ha alcanzado cada
continente?

``` r
gapminder %>%  group_by(continente) %>% 
                  summarise(max(expVida))
```

    ## # A tibble: 5 x 2
    ##   continente `max(expVida)`
    ##   <chr>               <dbl>
    ## 1 Africa               76.4
    ## 2 Americas             80.7
    ## 3 Asia                 82.6
    ## 4 Europe               81.8
    ## 5 Oceania              81.2

También podemos combinar el **group\_by** con **arrange**. Este último
*ordena* los datos.

Por ejemplo, ordenamos por Expectativa o Esperanza de Vida.

``` r
gapminder %>% 
    arrange(expVida) %>% head()
```

    ## # A tibble: 6 x 6
    ##   pais          year expVida    pobl PBI_PC continente
    ##   <chr>        <dbl>   <dbl>   <dbl>  <dbl> <chr>     
    ## 1 Rwanda        1992    23.6 7290203   737. Africa    
    ## 2 Afghanistan   1952    28.8 8425333   779. Asia      
    ## 3 Gambia        1952    30    284320   485. Africa    
    ## 4 Angola        1952    30.0 4232095  3521. Africa    
    ## 5 Sierra Leone  1952    30.3 2143249   880. Africa    
    ## 6 Afghanistan   1957    30.3 9240934   821. Asia

Vemos que Rwanda es el pais con expectativa de vida mas bajo en 1992 con
23 años\! Tiene sentido? Claro: Rwanda enfrentó una crisis alimentaria a
fines de la decada de 1980; estuvo en guerra a principios de 1990 y tuvo
distintos conflictos internos que terminarian en el genocidio de 1994.
La mayoria de los países con esperanza mas baja estuvieron en guerra en
esos años…y son todos de Africa y Asia.

Si nos enfocamos en Rwanda, podemos ver que la decada de 1990 esta
signada por los conflictos mencionados.

``` r
gapminder %>% 
    arrange(expVida) %>% 
    filter(pais == "Rwanda") %>% head()
```

    ## # A tibble: 6 x 6
    ##   pais    year expVida    pobl PBI_PC continente
    ##   <chr>  <dbl>   <dbl>   <dbl>  <dbl> <chr>     
    ## 1 Rwanda  1992    23.6 7290203   737. Africa    
    ## 2 Rwanda  1997    36.1 7212583   590. Africa    
    ## 3 Rwanda  1952    40   2534927   493. Africa    
    ## 4 Rwanda  1957    41.5 2822082   540. Africa    
    ## 5 Rwanda  1962    43   3051242   597. Africa    
    ## 6 Rwanda  2002    43.4 7852401   786. Africa

?Y la mayor expectativa? Simplemente pedimos un **arrange** pero al
reves.

``` r
gapminder %>% arrange(desc(expVida)) %>% head()
```

    ## # A tibble: 6 x 6
    ##   pais              year expVida      pobl PBI_PC continente
    ##   <chr>            <dbl>   <dbl>     <dbl>  <dbl> <chr>     
    ## 1 Japan             2007    82.6 127467972 31656. Asia      
    ## 2 Hong Kong, China  2007    82.2   6980412 39725. Asia      
    ## 3 Japan             2002    82   127065841 28605. Asia      
    ## 4 Iceland           2007    81.8    301931 36181. Europe    
    ## 5 Switzerland       2007    81.7   7554661 37506. Europe    
    ## 6 Hong Kong, China  2002    81.5   6762476 30209. Asia

Ahi estan los paises con mayor esperanza de vida. Todos del siglo XXI.

## Contar = count

Sencillamente, el **count** nos permite realizar un conteo de las
variables que queramos.

Por ejemplo, ?cuantos paises hay por continente?

``` r
count(gapminder, continente)
```

    ## # A tibble: 5 x 2
    ##   continente     n
    ##   <chr>      <int>
    ## 1 Africa       624
    ## 2 Americas     300
    ## 3 Asia         396
    ## 4 Europe       360
    ## 5 Oceania       24

## Cambiar el dataframe = spread

A veces necesitamos que cada variable tenga su propia columna, para
poder trabajar con ella o realizar determinadas visualizaciones (por
ejemplo el *heatmap*).

Para hacer esto, necesitamos utilizar algo que *extienda* la base\! Esto
se obtiene a traves del **spread**.

Por ejemplo, queremos que cada continente sea una variable que contenga
la expectativa de vida. De este modo, utilizamos el spread en el que la
variable ( **key** ) va a ser *continente* y el valor ( **value** ),
*expVida*.

``` r
extendido <- spread(gapminder, key = continente, value = expVida)

head(extendido)
```

    ## # A tibble: 6 x 9
    ##   pais         year     pobl PBI_PC Africa Americas  Asia Europe Oceania
    ##   <chr>       <dbl>    <dbl>  <dbl>  <dbl>    <dbl> <dbl>  <dbl>   <dbl>
    ## 1 Afghanistan  1952  8425333   779.     NA       NA  28.8     NA      NA
    ## 2 Afghanistan  1957  9240934   821.     NA       NA  30.3     NA      NA
    ## 3 Afghanistan  1962 10267083   853.     NA       NA  32.0     NA      NA
    ## 4 Afghanistan  1967 11537966   836.     NA       NA  34.0     NA      NA
    ## 5 Afghanistan  1972 13079460   740.     NA       NA  36.1     NA      NA
    ## 6 Afghanistan  1977 14880372   786.     NA       NA  38.4     NA      NA

## Exportar y guardar nuestro trabajo

Volvamos al principio y aprendamos a cargar las bases de datos. En este
caso, tenemos archivos CSV.

Si queremos guardar el dataframe que hicimos, por ejemplo el
*gapminder*, tenemos que usar **write**. En este caso, vamos a guardarlo
como archivo CSV.

``` r
write_csv(gapminder, "gapminder.csv")
```

Para traer el dataset, necesitamos usar un **read\_csv**. Primero, lo
asignamos asi aparece en nuestro Enviroment. Luego, llamamos al csv.

``` r
gapminder <- read_csv("gapminder.csv")
```
