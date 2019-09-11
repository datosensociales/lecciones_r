Clase 5 - Estructuras de control
================
Sofia Santamarina y Manuel Zapico
7/9/2019

Hoy vamos a ver las llamadas **estructuras de control**. Estas nos
permiten controlar la manera en que se ejecuta nuestro código.

Las estructuras de control establecen condicionales en nuestros código.
Por ejemplo, qué condiciones deben cumplirse para realizar una operación
o qué debe ocurrir para ejecutar una función.

Esto es de gran utilidad para determinar la lógica y el orden en que
ocurren las operaciones, en especial al definir funciones.

Las estructuras de control más usadas en R son las
siguientes:

| Estructura de control | Descripción                                                                                      |
| --------------------- | ------------------------------------------------------------------------------------------------ |
| if, else              | Si,de otro modo. Permite decidir si ejecutar o no un fragmento de código a partir una condición. |
| for                   | Para cada uno en. Ejecuta un bucle una cantidad fija de veces                                    |
| while                 | Mientras. Ejecuta un bucle mientras sea verdadera una condición                                  |
| break                 | Interrupción. Detiene la ejecución de un bucle                                                   |
| next                  | Siguiente. Salta a la siguiente ejecución de un bucle                                            |

Hoy nos centraremos en “if, else”. Veamos más detalladamente cómo se
usan:

*if* (si) es usado cuando deseamos que una operación se ejecute
únicamente cuando una condición se cumple.

*else* (de otro modo) es usado para indicarle a R qué hacer en caso de
la condición de un if no se cumpla.

Un *if* es la manera de decirle a R:

SI esta condición es cierta, ENTONCES haz estas operaciones.

``` r
if(Condicion) {
  operaciones_si_la_condicion_es_TRUE
}
```

Si la condición se cumple, es decir, es verdadera (TRUE), entonces se
realizan las operaciones. En caso contrario, no ocurre nada y el código
con las operaciones no es ejecutado.

Por ejemplo, le pedimos a R que nos muestre el texto “Verdadero” si la
condición se cumple.

``` r
# Se cumple la condición y se muestra "verdadero"

if(4 > 3) {
  "Verdadero"
}
```

    ## [1] "Verdadero"

``` r
# No se cumple la condición y no pasa nada

if(4 > 5) {
  "Verdadero"
}
```

Para que no suceda esto y nos arroje un resultado cuando la condición no
se cumple, usamos el **else** que complementa un **if**. El *else*
indica qué ocurrirá cuando la condición no se cumple, es falsa (FALSE),
en lugar de no hacer nada.

Un if con else es la manera de decirle a R:

*“SI esta condición es es cierta, ENTONCES haz estas operaciones, DE
OTRO MODO haz estas otras operaciones”*.

El modelo para un if con un else es:

``` r
if(condición) {
  operaciones_si_la_condición_es_TRUE
} else {
  operaciones_si_la_condición_es_FALSE
}
```

Usando los ejemplos anteriores, podemos mostrar “Falso” si no se cumple
la condición, en lugar de que no ocurra nada.

``` r
# Se cumple la condición y se muestra "Verdadero"
if(4 > 3) {
  "Verdadero"
} else {
  "Falso"
}
```

    ## [1] "Verdadero"

``` r
# No se cumple la condición y se muestra "Falso"

if(4 > 5) {
  "Verdadero"
} else {
  "Falso"
}
```

    ## [1] "Falso"

*Ejercicio*: A partir del dataset “encuesta” del paquete “datos” le
pedimos a R que nos muestre aquellas personas consideradas “Muy
creyentes” según la cantidad de horas de tv que miran. Es decir, le
pedimos a R que nos muestre el texto “Muy creyente” si cumple la
condición de mirar más de 4 horas tv religiosa.

``` r
#Primero, cargamos los paquetes de "tidyverse" y "datos" 
#Luego elegimos el dataset de "encuestas"

library(tidyverse)
```

    ## Registered S3 method overwritten by 'rvest':
    ##   method            from
    ##   read_xml.response xml2

    ## -- Attaching packages --------------------------- tidyverse 1.2.1.9000 --

    ## v ggplot2 3.2.0       v purrr   0.3.2  
    ## v tibble  2.1.1       v dplyr   0.8.0.1
    ## v tidyr   0.8.3       v stringr 1.4.0  
    ## v readr   1.3.1       v forcats 0.4.0

    ## -- Conflicts ----------------------------------- tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(datos)
```

    ## Warning: package 'datos' was built under R version 3.6.1

``` r
encuesta <- datos::encuesta

encuesta
```

    ## # A tibble: 21,483 x 9
    ##     anio estado_civil  edad raza  ingreso partido religion denominacion
    ##    <int> <fct>        <int> <fct> <fct>   <fct>   <fct>    <fct>       
    ##  1  2000 Nunca se ha~    26 Blan~ 8000 -~ Indepe~ Protest~ Bautistas d~
    ##  2  2000 Divorciado      48 Blan~ 8000 -~ Republ~ Protest~ Bautista, n~
    ##  3  2000 Viudo           67 Blan~ No apl~ Indepe~ Protest~ No denomina~
    ##  4  2000 Nunca se ha~    39 Blan~ No apl~ Indepe~ Cristia~ No aplica   
    ##  5  2000 Divorciado      25 Blan~ No apl~ Demócr~ Ninguna  No aplica   
    ##  6  2000 Casado          25 Blan~ 20000 ~ Demócr~ Protest~ Bautistas d~
    ##  7  2000 Nunca se ha~    36 Blan~ 25000 ~ Republ~ Cristia~ No aplica   
    ##  8  2000 Divorciado      44 Blan~ 7000 -~ Indepe~ Protest~ Sínodo lute~
    ##  9  2000 Casado          44 Blan~ 25000 ~ Demócr~ Protest~ Otra        
    ## 10  2000 Casado          47 Blan~ 25000 ~ Republ~ Protest~ Bautistas d~
    ## # ... with 21,473 more rows, and 1 more variable: horas_tv <int>

``` r
if(encuesta$horas_tv > 4) print("Muy creyente")
```

Este mensaje nos dice que sólo se usará el primer elemento del vector
para evaluar su la condición es verdadera y lo demás será ignorado.

Para resolver este problema, usamos el **ifelse** que nos devolverá un
valor para cada elemento delvector en el que la condición sea TRUE, y
además nos devolverá otro valor para los elementos en que la condición
sea FALSE.

Esta función tiene la siguiente forma.

``` r
ifelse(vector, valor_si_TRUE, valor_si_FALSE)
```

Si intentamos el ejemplo anterior con ifelse(), se nos devolverá un
resultado para cada elemento del vector, no sólo del primero de ellos.

``` r
ifelse(encuesta$horas_tv > 4, "Muy creyente", "Poco creyente") %>% 
  head(40)
```

    ##  [1] "Muy creyente"  NA              "Poco creyente" "Poco creyente"
    ##  [5] "Poco creyente" NA              "Poco creyente" NA             
    ##  [9] "Poco creyente" "Poco creyente" "Poco creyente" NA             
    ## [13] "Poco creyente" NA              "Poco creyente" "Muy creyente" 
    ## [17] NA              "Poco creyente" "Poco creyente" NA             
    ## [21] "Poco creyente" "Poco creyente" "Poco creyente" "Poco creyente"
    ## [25] "Poco creyente" NA              "Poco creyente" NA             
    ## [29] "Muy creyente"  NA              "Poco creyente" NA             
    ## [33] "Poco creyente" NA              NA              NA             
    ## [37] "Poco creyente" "Poco creyente" "Poco creyente" "Poco creyente"

``` r
#Eliminamos los "NA" 

encuesta <- filter(encuesta, horas_tv != "NA")

ifelse(encuesta$horas_tv > 4, "Muy creyente", "Poco creyente") %>% 
  head(40)
```

    ##  [1] "Muy creyente"  "Poco creyente" "Poco creyente" "Poco creyente"
    ##  [5] "Poco creyente" "Poco creyente" "Poco creyente" "Poco creyente"
    ##  [9] "Poco creyente" "Poco creyente" "Muy creyente"  "Poco creyente"
    ## [13] "Poco creyente" "Poco creyente" "Poco creyente" "Poco creyente"
    ## [17] "Poco creyente" "Poco creyente" "Poco creyente" "Muy creyente" 
    ## [21] "Poco creyente" "Poco creyente" "Poco creyente" "Poco creyente"
    ## [25] "Poco creyente" "Poco creyente" "Poco creyente" "Poco creyente"
    ## [29] "Poco creyente" "Poco creyente" "Poco creyente" "Muy creyente" 
    ## [33] "Poco creyente" "Poco creyente" "Poco creyente" "Poco creyente"
    ## [37] "Poco creyente" "Poco creyente" "Poco creyente" "Poco creyente"

``` r
#Ahora veamos el promedio de horas_tv según partido politico de las personas, y averiguemos en cuál partido están los más creyentes. 

#Primero reacomodamos los datos para tener el promedio de horas por partido politico

tv_partido <- encuesta %>% #tomamos el dataset
              group_by(partido) %>% #agrupamos por partido
              summarise(prom_tv = round(mean(horas_tv), 2)) %>% #calculamos la media por partido. A la nueva variable la llamamos prom_tv y le pido solo 2 decimales a partir de la funcion "round, 2"
              arrange(desc(prom_tv)) #ordenamos en forma decreciente
```

Usamos la funcion **“paste0()”** para que el resultado sea más
explicativo. Esta función acepta como argumentos cadenas de texto y las
pega (concatena) entre sí, devolviendo como resultado una nueva cadena.

``` r
#Armamos la condición con "ifelse" ya que se trata de un vector 

{
  partido <- tv_partido$partido 
  media <- tv_partido$prom_tv
  texto <- paste0(partido,  ", " , media, ", ")

ifelse(media > 4,
    print(paste0(texto, "Muy creyente")), 
    print(paste0(texto, "Poco creyente")))
  }
```

    ##  [1] "Demócrata duro, 3.52, Poco creyente"               
    ##  [2] "Sin respuesta, 3.22, Poco creyente"                
    ##  [3] "Independiente, 3.08, Poco creyente"                
    ##  [4] "Demócrata moderado, 3.04, Poco creyente"           
    ##  [5] "Independiente pro demócrata, 2.8, Poco creyente"   
    ##  [6] "Otro partido, 2.79, Poco creyente"                 
    ##  [7] "Independiente pro republicano, 2.77, Poco creyente"
    ##  [8] "Republicano duro, 2.72, Poco creyente"             
    ##  [9] "Republicano moderado, 2.63, Poco creyente"         
    ## [10] "No sabe, 2, Poco creyente"

    ##  [1] "Demócrata duro, 3.52, Poco creyente"               
    ##  [2] "Sin respuesta, 3.22, Poco creyente"                
    ##  [3] "Independiente, 3.08, Poco creyente"                
    ##  [4] "Demócrata moderado, 3.04, Poco creyente"           
    ##  [5] "Independiente pro demócrata, 2.8, Poco creyente"   
    ##  [6] "Otro partido, 2.79, Poco creyente"                 
    ##  [7] "Independiente pro republicano, 2.77, Poco creyente"
    ##  [8] "Republicano duro, 2.72, Poco creyente"             
    ##  [9] "Republicano moderado, 2.63, Poco creyente"         
    ## [10] "No sabe, 2, Poco creyente"

Vemos que ningún partido supera el umbral de 4 horas que establecimos,
asique calculemos el promedio general y usemos ese dato como umbral.

``` r
umbral <- datos::encuesta

umbral <- filter(umbral, horas_tv != "NA")

mean(umbral$horas_tv) 
```

    ## [1] 2.980771

Entonces, el umbral es de 2.98. Calculemos nuevamente las condiciones
con *ifelse*, según partido político y las horas que miran tv.

``` r
{
  partido <- tv_partido$partido 
  media <- tv_partido$prom_tv
  texto <- paste0(partido,  ", " , media, ", ")

ifelse(media >= 2.98,
    print(paste0(texto, "Muy creyente")), 
    print(paste0(texto, "Poco creyente")))
}
```

    ##  [1] "Demócrata duro, 3.52, Muy creyente"               
    ##  [2] "Sin respuesta, 3.22, Muy creyente"                
    ##  [3] "Independiente, 3.08, Muy creyente"                
    ##  [4] "Demócrata moderado, 3.04, Muy creyente"           
    ##  [5] "Independiente pro demócrata, 2.8, Muy creyente"   
    ##  [6] "Otro partido, 2.79, Muy creyente"                 
    ##  [7] "Independiente pro republicano, 2.77, Muy creyente"
    ##  [8] "Republicano duro, 2.72, Muy creyente"             
    ##  [9] "Republicano moderado, 2.63, Muy creyente"         
    ## [10] "No sabe, 2, Muy creyente"                         
    ##  [1] "Demócrata duro, 3.52, Poco creyente"               
    ##  [2] "Sin respuesta, 3.22, Poco creyente"                
    ##  [3] "Independiente, 3.08, Poco creyente"                
    ##  [4] "Demócrata moderado, 3.04, Poco creyente"           
    ##  [5] "Independiente pro demócrata, 2.8, Poco creyente"   
    ##  [6] "Otro partido, 2.79, Poco creyente"                 
    ##  [7] "Independiente pro republicano, 2.77, Poco creyente"
    ##  [8] "Republicano duro, 2.72, Poco creyente"             
    ##  [9] "Republicano moderado, 2.63, Poco creyente"         
    ## [10] "No sabe, 2, Poco creyente"

    ##  [1] "Demócrata duro, 3.52, Muy creyente"                
    ##  [2] "Sin respuesta, 3.22, Muy creyente"                 
    ##  [3] "Independiente, 3.08, Muy creyente"                 
    ##  [4] "Demócrata moderado, 3.04, Muy creyente"            
    ##  [5] "Independiente pro demócrata, 2.8, Poco creyente"   
    ##  [6] "Otro partido, 2.79, Poco creyente"                 
    ##  [7] "Independiente pro republicano, 2.77, Poco creyente"
    ##  [8] "Republicano duro, 2.72, Poco creyente"             
    ##  [9] "Republicano moderado, 2.63, Poco creyente"         
    ## [10] "No sabe, 2, Poco creyente"

Podemos concluir que los demócratas (duros o moderados) son más
creyentes que los republicanos.

-----

ifelse es útil para recodificar datos, combiandolo con la funcion
**mutate**.

Creemos una nueva columna que se llame “Tipo\_creyente”.

``` r
#encuesta <- filter(encuesta, horas_tv != "NA")

encuesta<- encuesta %>% 
  mutate(Tipo_creyente = ifelse(horas_tv > 2.98, "Muy creyente", "Poco creyente")) 

head(encuesta) 
```

    ## # A tibble: 6 x 10
    ##    anio estado_civil  edad raza  ingreso partido religion denominacion
    ##   <int> <fct>        <int> <fct> <fct>   <fct>   <fct>    <fct>       
    ## 1  2000 Nunca se ha~    26 Blan~ 8000 -~ Indepe~ Protest~ Bautistas d~
    ## 2  2000 Viudo           67 Blan~ No apl~ Indepe~ Protest~ No denomina~
    ## 3  2000 Nunca se ha~    39 Blan~ No apl~ Indepe~ Cristia~ No aplica   
    ## 4  2000 Divorciado      25 Blan~ No apl~ Demócr~ Ninguna  No aplica   
    ## 5  2000 Nunca se ha~    36 Blan~ 25000 ~ Republ~ Cristia~ No aplica   
    ## 6  2000 Casado          44 Blan~ 25000 ~ Demócr~ Protest~ Otra        
    ## # ... with 2 more variables: horas_tv <int>, Tipo_creyente <chr>

Tenemos una nueva columna que clasifica cada unidad en “Muy creyente” y
en “Poco creyente”. Pero podriamos refinar aún más la categoria y
agregar dos condiciones para clasificar, por ejemplo, a partir de la
religión declarada.

``` r
encuesta <- encuesta %>% 
  mutate(Tipo_creyente = ifelse(horas_tv > 2.98 & religion != "Ninguna", "Muy creyente", "Poco creyente")) 

head(encuesta, 20) 
```

    ## # A tibble: 20 x 10
    ##     anio estado_civil  edad raza  ingreso partido religion denominacion
    ##    <int> <fct>        <int> <fct> <fct>   <fct>   <fct>    <fct>       
    ##  1  2000 Nunca se ha~    26 Blan~ 8000 -~ Indepe~ Protest~ Bautistas d~
    ##  2  2000 Viudo           67 Blan~ No apl~ Indepe~ Protest~ No denomina~
    ##  3  2000 Nunca se ha~    39 Blan~ No apl~ Indepe~ Cristia~ No aplica   
    ##  4  2000 Divorciado      25 Blan~ No apl~ Demócr~ Ninguna  No aplica   
    ##  5  2000 Nunca se ha~    36 Blan~ 25000 ~ Republ~ Cristia~ No aplica   
    ##  6  2000 Casado          44 Blan~ 25000 ~ Demócr~ Protest~ Otra        
    ##  7  2000 Casado          47 Blan~ 25000 ~ Republ~ Protest~ Bautistas d~
    ##  8  2000 Casado          53 Blan~ 25000 ~ Demócr~ Protest~ Otra        
    ##  9  2000 Casado          52 Blan~ 25000 ~ Demócr~ Protest~ Bautistas d~
    ## 10  2000 Divorciado      52 Blan~ 25000 ~ Indepe~ Ninguna  No aplica   
    ## 11  2000 Casado          40 Negra 25000 ~ Demócr~ Protest~ Bautista, n~
    ## 12  2000 Nunca se ha~    44 Blan~ 25000 ~ Indepe~ Ninguna  No aplica   
    ## 13  2000 Casado          40 Blan~ 10000 ~ Demócr~ Católica No aplica   
    ## 14  2000 Casado          48 Blan~ 25000 ~ Indepe~ Católica No aplica   
    ## 15  2000 Casado          49 Blan~ Se nie~ Republ~ Protest~ Iglesia met~
    ## 16  2000 Nunca se ha~    19 Blan~ No apl~ Indepe~ Ninguna  No aplica   
    ## 17  2000 Viudo           54 Blan~ 25000 ~ Indepe~ Cristia~ No aplica   
    ## 18  2000 Viudo           82 Blan~ No apl~ Demócr~ Protest~ Otra        
    ## 19  2000 Viudo           89 Blan~ No apl~ Demócr~ Protest~ Otras luter~
    ## 20  2000 Divorciado      72 Blan~ No apl~ Demócr~ Protest~ Bautistas d~
    ## # ... with 2 more variables: horas_tv <int>, Tipo_creyente <chr>

Si revisamos los atos, observamos que al valor “religion == Ninguna” le
asigna “Poco Creyente”, sin importar las “horas\_tv”. Sin embargo, para
ser aun más especificos, deberia ser clasificado con otra categoria,
como “Creyente simpatizante”.

Para eso, vamos a utilizar **case\_when()**, una función particularmente
útil dentro de mutate para crear una nueva variable que dependa de una
combinación compleja de variables existentes.

``` r
encuesta <- encuesta %>% 
  mutate(Tipo_creyente = case_when(religion == "Ninguna" ~ "Creyente Simpatizante", 
                                   horas_tv >= 2.98 ~ "Muy creyente",
                                   TRUE ~ "Poco creyente")) #TRUE es equivalente al "else" 

head(encuesta, 20)
```

    ## # A tibble: 20 x 10
    ##     anio estado_civil  edad raza  ingreso partido religion denominacion
    ##    <int> <fct>        <int> <fct> <fct>   <fct>   <fct>    <fct>       
    ##  1  2000 Nunca se ha~    26 Blan~ 8000 -~ Indepe~ Protest~ Bautistas d~
    ##  2  2000 Viudo           67 Blan~ No apl~ Indepe~ Protest~ No denomina~
    ##  3  2000 Nunca se ha~    39 Blan~ No apl~ Indepe~ Cristia~ No aplica   
    ##  4  2000 Divorciado      25 Blan~ No apl~ Demócr~ Ninguna  No aplica   
    ##  5  2000 Nunca se ha~    36 Blan~ 25000 ~ Republ~ Cristia~ No aplica   
    ##  6  2000 Casado          44 Blan~ 25000 ~ Demócr~ Protest~ Otra        
    ##  7  2000 Casado          47 Blan~ 25000 ~ Republ~ Protest~ Bautistas d~
    ##  8  2000 Casado          53 Blan~ 25000 ~ Demócr~ Protest~ Otra        
    ##  9  2000 Casado          52 Blan~ 25000 ~ Demócr~ Protest~ Bautistas d~
    ## 10  2000 Divorciado      52 Blan~ 25000 ~ Indepe~ Ninguna  No aplica   
    ## 11  2000 Casado          40 Negra 25000 ~ Demócr~ Protest~ Bautista, n~
    ## 12  2000 Nunca se ha~    44 Blan~ 25000 ~ Indepe~ Ninguna  No aplica   
    ## 13  2000 Casado          40 Blan~ 10000 ~ Demócr~ Católica No aplica   
    ## 14  2000 Casado          48 Blan~ 25000 ~ Indepe~ Católica No aplica   
    ## 15  2000 Casado          49 Blan~ Se nie~ Republ~ Protest~ Iglesia met~
    ## 16  2000 Nunca se ha~    19 Blan~ No apl~ Indepe~ Ninguna  No aplica   
    ## 17  2000 Viudo           54 Blan~ 25000 ~ Indepe~ Cristia~ No aplica   
    ## 18  2000 Viudo           82 Blan~ No apl~ Demócr~ Protest~ Otra        
    ## 19  2000 Viudo           89 Blan~ No apl~ Demócr~ Protest~ Otras luter~
    ## 20  2000 Divorciado      72 Blan~ No apl~ Demócr~ Protest~ Bautistas d~
    ## # ... with 2 more variables: horas_tv <int>, Tipo_creyente <chr>

Tenemos 3 categorias para “Tipo\_creyente”. Pero aun asi, no todos los
“Creyentes Simpatizantes” son iguales, ya que algunos miran muchas más
horas de tv que otros. Calculamos el promedio de horas de tv que mira
este sub conjunto de personas.

``` r
simpatizantes <- encuesta %>% 
  filter(Tipo_creyente == "Creyente Simpatizante")

mean(simpatizantes$horas_tv)
```

    ## [1] 2.710227

``` r
encuesta <- encuesta %>% 
  mutate(Tipo_creyente = case_when(religion == "Ninguna" & horas_tv >= 2.7 ~ "Simpatizante comprometido", 
                                   religion == "Ninguna" & horas_tv <= 2.7 ~ "Simpatizante debil",
                                   religion != "Ninguna" & horas_tv >= 2.98 ~ "Muy creyente",
                                   religion != "Ninguna" & horas_tv <= 2.98 ~ "Poco creyente"))

head(encuesta, 30)
```

    ## # A tibble: 30 x 10
    ##     anio estado_civil  edad raza  ingreso partido religion denominacion
    ##    <int> <fct>        <int> <fct> <fct>   <fct>   <fct>    <fct>       
    ##  1  2000 Nunca se ha~    26 Blan~ 8000 -~ Indepe~ Protest~ Bautistas d~
    ##  2  2000 Viudo           67 Blan~ No apl~ Indepe~ Protest~ No denomina~
    ##  3  2000 Nunca se ha~    39 Blan~ No apl~ Indepe~ Cristia~ No aplica   
    ##  4  2000 Divorciado      25 Blan~ No apl~ Demócr~ Ninguna  No aplica   
    ##  5  2000 Nunca se ha~    36 Blan~ 25000 ~ Republ~ Cristia~ No aplica   
    ##  6  2000 Casado          44 Blan~ 25000 ~ Demócr~ Protest~ Otra        
    ##  7  2000 Casado          47 Blan~ 25000 ~ Republ~ Protest~ Bautistas d~
    ##  8  2000 Casado          53 Blan~ 25000 ~ Demócr~ Protest~ Otra        
    ##  9  2000 Casado          52 Blan~ 25000 ~ Demócr~ Protest~ Bautistas d~
    ## 10  2000 Divorciado      52 Blan~ 25000 ~ Indepe~ Ninguna  No aplica   
    ## # ... with 20 more rows, and 2 more variables: horas_tv <int>,
    ## #   Tipo_creyente <chr>

Finalmente, tenemos 4 “Tipo\_creyente” según la religión que practica y
la cantidad de “horas\_tv” que mira.
