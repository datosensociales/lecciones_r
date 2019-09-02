CLASE 2
================
August 1, 2019

## DATOS Y OBJETOS

### DATOS

Empezamos este curso viendo que tipo de datos tenemos en R.

Los datos mas comunes -y los que vamos a usar en este curso- son tres:
**Numericos** (*numerics*) **Caracteres** (*character*) **Vectoriales**
(*vectors*)

Para saber que tipo de datos tenemos en un *dataframe* o en un *objeto*,
es fundamental la funcion **CLASS**

Por ejemplo, al ver numericos o categoricos:

Noten que puse *arbol* entre comillas. Esto es fundamental, ya que es
una forma de identificar un *character*. Por ejemplo, si elijo un numero
y lo pongo entre comillas…

``` r
class("3")
```

    ## [1] "character"

Estos tipos de datos son los mas importantes. **R** puede ser usado como
una calculadora de datos numericos:

``` r
40/4
```

    ## [1] 10

``` r
30+34*12-15
```

    ## [1] 423

``` r
sqrt(9)
```

    ## [1] 3

### Objetos

Antes de ver el tercer tipo de datos, tenemos que deternos a conocer los
**objetos**. Ellos son lo que en otros programas son llamados
**variables**. Basicamente constituyen un elemento al que le asignamos
valores. Aparecera en nuestro *Enviroment* y lo hacemos usando el
comando `<-`

``` r
x <- 45
```

Ya lo asignamos y aparece en el Enviroment. Para que aparezca en nuestro
Script, debemos “llamarlo”

``` r
x
```

    ## [1] 45

Una vez hecho esto, el *x* tendrá SIEMPRE ese valor de 45. **SALVO** que
asignemos mas abajo otro valor de nombre *x*. Asi se pueden hacer
cuentas de este estilo:

``` r
sqrt(x)
```

    ## [1] 6.708204

``` r
x-40
```

    ## [1] 5

``` r
x/2 + 50
```

    ## [1] 72.5

La raiz cuadrada **sqrt()** de 45 deja muchos decimales. Se puede
reducir? CLARO\! Si tenemos esa duda, googleamos la pregunta y nos va a
decir que usemos **round**.

``` r
sqrt(x)
```

    ## [1] 6.708204

``` r
round(sqrt(x))
```

    ## [1] 7

El resultado da 7. Si lo queremos con un par de decimales, podemos
pedirlo. Googleamos o vamos a la parte de la consola y ponemos ?round.
Este signo de pregunta nos va a abrir el panel “help” y nos explica
cuales son los atributos de la funcion. Digamos que lo quiero con dos
decimales:

``` r
round(sqrt(x), 2)
```

    ## [1] 6.71

Veamos el largo que posee el siguiente objeto de **class()**
*character*

``` r
y <- "en el medio del camino de nuestra vida, me encontre en una selva oscura"
length(y)
```

    ## [1] 1

¿Por qué \[1\]? Porque considera que es un solo valor, sin importar su
extension. Una coleccion de datos del mismo tipo es lo que se conoce
como un **VECTOR** que es lo que veremos a continuacion. Para construir
un vector, debemos crear un objeto y los valores ponerlos despues de
*c()*

### Vectores numéricos

``` r
VecNum <- c(32, 33, 36, 45, 68, 87, 90, 120, 122, 145, 178)

class(VecNum)
```

    ## [1] "numeric"

``` r
length(VecNum)
```

    ## [1] 11

Como podemos ver, nuestro vector es numérico y el objeto esta compuesto
por distintos valores que ahora se puede diferenciar. Por ejemplo, ¿cómo
selecciono el cuarto valor?

``` r
VecNum[4]
```

    ## [1] 45

Mostrame desde el primer valor al sexto

``` r
VecNum[1:6]
```

    ## [1] 32 33 36 45 68 87

Sumemos “15” a los valores

``` r
VecNum+15
```

    ##  [1]  47  48  51  60  83 102 105 135 137 160 193

Restemos “15”

``` r
VecNum-15
```

    ##  [1]  17  18  21  30  53  72  75 105 107 130 163

¿Cuántos valores tenemos en total?

``` r
length(VecNum)
```

    ## [1] 11

Si usamos la funcion head nos da los primeros 6 valores. La funcion
“tail” es para que nos muestre los ultimos 6.

``` r
head(VecNum)
```

    ## [1] 32 33 36 45 68 87

``` r
tail(VecNum)
```

    ## [1]  87  90 120 122 145 178

Dame todos los valores menos el segundo (33)

``` r
VecNum-33
```

    ##  [1]  -1   0   3  12  35  54  57  87  89 112 145

¿Qué pasa? Esta interpretando que debo restarle 33 a TODOS los valores\!
Lo que tengo que hacer es que me reste el SEGUNDO valor (que es 33) y
poner entre corchetes para que sepa que quiero sacar esa variable

``` r
VecNum [-2]
```

    ##  [1]  32  36  45  68  87  90 120 122 145 178

Quiero cambiar el octavo numero de la lista por “121”

``` r
VecNum[8] <- 121
VecNum
```

    ##  [1]  32  33  36  45  68  87  90 121 122 145 178

Si quiero verlo en formato de tabla y fuera de este panel utilizamos la
función `View()`. Nos lo abre en otra “pestaña” View(VecNum)

### Vectores lógicos

Otros tipos de vectores son los logicos o booleanos. Estos son
fundamentales para saber si un valores es *verdadero*(TRUE) o
*falso*(FALSE) segun la funcion que le pidamos. Mas adelante veremos que
es fundamental para usar, por ejemplo, las funciones del paquete
**tidyverse**.

Digamos que quiero saber cuáles son los valores de mi Objeto mayores de
40.

``` r
VectorLogico <- VecNum >= 40
VectorLogico
```

    ##  [1] FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE

``` r
class(VectorLogico)
```

    ## [1] "logical"

Los operadores lógicos son:

**MAYOR A** \> *y* \>= **MENOR A** \< *y* \<= **IGUAL A** == *atencion
con el doble igual* **DISTINTO A** \!= **VALOR Y OTRO VALOR** & **VALOR
U OTRO VALOR** |

Se puede hacer con dos vectores también:

``` r
VecNum2 <- c(32, 33, 36, 45, 70, 94, 100, 120, 122, 158, 179)

VecNum == VecNum2
```

    ##  [1]  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE  TRUE FALSE FALSE

### Vectores de caracteres (**strings**)

Ademas de *numericos* podemos armar vectores de caracteres o **strings**

``` r
VectorString <- c("perro", "gato", "raton", "pajaro", "pez")

length(VectorString)
```

    ## [1] 5

``` r
class(VectorString)
```

    ## [1] "character"

Por ejemplo, queremos elegir la inicial de cada animal para usarla
despues. Usamos **substr()**

``` r
substr(VectorString, start= 1, stop = 1)
```

    ## [1] "p" "g" "r" "p" "p"

Con las indicaciones de “start” y “stop” le indicamos cu?ntas letras
queremos que nos muestre de cada palabra. POr ejemplo:

``` r
substr(VectorString, start = 1, stop = 2)
```

    ## [1] "pe" "ga" "ra" "pa" "pe"

``` r
substr(VectorString, start = 1, stop = 3)
```

    ## [1] "per" "gat" "rat" "paj" "pez"

Con **grep** tomamos algunos valores de los vectores character.

``` r
VectorString[grep(pattern = "r", x = VectorString)]
```

    ## [1] "perro"  "raton"  "pajaro"

Hagamos un nuevo objeto con los animales con “r”

``` r
ConR <- VectorString[grep(pattern = "r", x = VectorString)]
ConR
```

    ## [1] "perro"  "raton"  "pajaro"

## Valores NA

Muchas veces, al abrir un archivo o **dataset** (lo veremos en la
Clase\_2), puede ser que tengamos *missing values*, es decir, que no
haya valores. Esto en R se representa con un **NA**. El problema con
este valor es que puede afectar las funciones que queramos realizar,
como la sumatoria de todo, el promedio, el valor maximo, etc. Por lo
tanto, muchas veces debemos saltear, sacar o asignar un nuevo valor al
**NA**. ?Como lo hacemos?

Por ejemplo, el siguiente vector contiene una serie de precios con un
*missing value*:

``` r
precios <- c(25, 67, 21, 54, 899, 23, NA, 34, 56)
```

Veamos que pasa si pedimos la sumatoria de precios, el valor maximo y el
promedio:

``` r
sum(precios)
```

    ## [1] NA

``` r
max(precios)
```

    ## [1] NA

``` r
mean(precios)
```

    ## [1] NA

Primero vamos a **ignorar** el valor **NA** usando *na.rm*:

``` r
sum(precios, na.rm = TRUE)
```

    ## [1] 1179

``` r
max(precios, na.rm = TRUE)
```

    ## [1] 899

``` r
mean(precios, na.rm = TRUE)
```

    ## [1] 147.375

``` r
round(mean(precios, na.rm = TRUE)) #Practicamos el round ;) 
```

    ## [1] 147

Ahora bien, supongamos que tenemos muchos **NA** en nuestro dataset y
queremos sacarlos para que no interfieran con nuestro análisis. Vamos a
usar **is.na** que es la funcion para identificar los **NA** PERO vamos
a agregarle el “\!” que, como vimos es la funcion logica de “lo distinto
a”. Así, estamos diciendo “selecciona lo distinto a NA”.

Selecciona cuando “es” -is- NA

``` r
precios[is.na(precios)]
```

    ## [1] NA

Ahora seleccionamos lo “diferente” a is.na

``` r
precios[!is.na(precios)]
```

    ## [1]  25  67  21  54 899  23  34  56

Para tenerlo en un dataset, podemos asignarlo a un objeto:

``` r
precios_sin_NA <- precios[!is.na(precios)]

precios_sin_NA
```

    ## [1]  25  67  21  54 899  23  34  56

Por ultimo, a veces es necesario no eliminar el NA sino reemplazarlo por
otro valor, generalmente 0. ?Como hacemos esto? Sencillamente, en lugar
de construir un objeto nuevo, le pedimos que modifique algo de uno ya
existente. Identificamos los NA con is.na y pedimos que cambie los de
“PRECIOS” por 0.

``` r
precios[is.na(precios)] = 0

precios
```

    ## [1]  25  67  21  54 899  23   0  34  56

Eso es todo por hoy\!\!\!\!\!\!\!

> ## Exercise
> 
> 1.  Using this vector of rooms, create a new vector with the NAs
>     removed.
>     
>     ``` r
>     rooms <- c(1, 2, 1, 1, NA, 3, 1, 3, 2, 1, 1, 8, 3, 1, NA, 1)
>     ```
> 
> 2.  Use the function `median()` to calculate the median of the `rooms`
>     vector.
> 
> 3.  Use R to figure out how many households in the set use more than 2
>     rooms for sleeping.
> 
> > ## Solution
> > 
> > ``` r
> > rooms <- c(1, 2, 1, 1, NA, 3, 1, 3, 2, 1, 1, 8, 3, 1, NA, 1)
> > rooms_no_na <- rooms[!is.na(rooms)]
> > # or
> > rooms_no_na <- na.omit(rooms)
> > # 2.
> > median(rooms, na.rm = TRUE)
> > ```
> > 
> >     ## [1] 1
> > 
> > ``` r
> > # 3.
> > rooms_above_2 <- rooms_no_na[rooms_no_na > 2]
> > length(rooms_above_2)
> > ```
> > 
> >     ## [1] 4
> > 
> > {: .solution} {: .challenge}
