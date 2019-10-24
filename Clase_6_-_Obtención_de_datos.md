Clase 6 - Obtención de datos
================
Ciencia de datos en FSOC
16/9/2019

Datos Abiertos
--------------

Un recurso fundamental para la utilización es la **BASE DE DATOS**. Podemos obtenerlas de nuestros trabajos o sitios dedicados a publicar datos.

En los últimos años se ha fomentado la **apertura de datos**: esto quiere decir que gobiernos, organizaciones no gubernamentales, instituciones y hasta empresas privadas, publican datasets con información de su trabajo y relevamiento.

*No es ideal:* las bases de datos pueden contener información fragmentada o que hace difícil su utilización. Esto último puede solucionarse con “limpieza”, pero puede ser un trabajo complejo y que nos consume mucho tiempo.

#### Fuentes de datos abiertos: sitios internacionales

-   Datos abiertos del Banco Mundial <https://datacatalog.worldbank.org/>

-   Datos abiertos de la [Organización Internacional del Trabajo](https://www.ilo.org/ilostat/faces/wcnav_defaultSelection;ILOSTATCOOKIE=5mRXwKxS-ssNPzgNwjw_Fw1tmTsnJj45X3NN3l3bJ1E5k_RZzb2E!-612270756?_afrLoop=1551802768150004&_afrWindowMode=0&_afrWindowId=null#!%40%40%3F_afrWindowId%3Dnull%26_afrLoop%3D1551802768150004%26_afrWindowMode%3D0%26_adf.ctrl-state%3Dfr3yq4fzg_4)

-   Datos abiertos del World Value Survey <http://www.worldvaluessurvey.org/WVSContents.jsp>

-   Datos abiertos del PNUD <http://hdr.undp.org/en/data>

-   Datos abiertos del BANCO INTERAMERICANO DE DESARROLLO <https://data.iadb.org/DataCatalog/Dataset>

#### Fuentes de datos abiertos: sitios nacionales

-   Datos abiertos del INDEC <https://www.indec.gob.ar/indec/web/Institucional-Indec-BasesDeDatos>

-   Datos abiertos del CEDLAS <http://www.cedlas.econo.unlp.edu.ar/wp/estadisticas/lablac/links/>

-   Datos electorales DINE <https://www.argentina.gob.ar/interior/dine/resultadosyestadisticas>

-   Datos abiertos en DATOS ARGENTINA <https://datos.gob.ar/>

-   Datos BUENOS AIRES DATA <https://data.buenosaires.gob.ar/>

-   Datos Estadísticas y Censos CABA <https://www.estadisticaciudad.gob.ar/eyc/?page_id=35782>

-   Datos Defensoría del Pueblo CABA <http://datos.defensoria.org.ar/dataset-tramites/>

#### ¿Cómo cargarlos?

``` r
library(tidyverse)
#CSV

datos <- read_csv("dataset.csv")

#Excel 

datos <- readxl::read_xlsx("dataset.xlsx")
```

Conectarse a la API de twitter
------------------------------

Un **API (Application Programming Interface)** es la interfaz que un software utiliza para interactuar con otro software.

Un **Web API** es un API que se invoca a través del protocolo HTTP. La ventaja de usar HTTP es que es posible hacer peticiones desde cualquier lenguaje de programación, lo que hace a la Web un medio ideal para conectar aplicaciones.

Muchos sitios y aplicaciones Web (Facebook, Twitter, Github, Google Maps, LinkedIn, Youtube, etc.) exponen gran parte de su funcionalidad a través de API’s permitiendo extender su funcionalidad

#### ¿Cómo conectarse a la API de Twitter?

Para acceder a los sistemas de *Twitter* necesitamos obtener una autorización.

La autorización otorgada por twitter nos dará una serie de códigos de identificación, conocidos en su conjunto como **API keys**

-   Consumer Key
-   Consumer Secret
-   Acccess Token
-   Acccess Token Secret

Para conseguri esas API Keys necesitamos hacer un par de pasos:

1.  Tener una cuenta de twitter.
2.  Ir a <https://dev.twitter.com/> e ingresar con el usuario de twitter.
3.  Ingresar a <https://developer.twitter.com/en/apps> para crear tu App
4.  Una vez que Twitter te autoriza la app, al ingresar a tu propia aparecerá una pestaña llamada "Keys and Tokens". Alli estarán las claves que necesitamos, las anotamos para tenerlas a mano y poder trabajar en R.

Nos conectamos a la API de @TW desde R

``` r
API Keys
consumer_key <- "tu_cave_consumer_key"
consumer_secret <- "clave_consumer_secret"
access_token <- "clave_access_token"
access_secret <- "clave_access_secret"

setup_twitter_oauth(consumer_key, consumer_secret, access_token, access_secret)
```

#### Acceso a Twitter vía R: el paquete *rtweet*

A twitter podemos pedirle tres tipos de datos:

**timeline** de un usuario a partir de la función `get_timeline()`

``` r
usuario <- get_timeline("@usuario", since = "fecha", n=50000)
```

tweets que contengan una **palabra** - o varias - o un **hashtag** específico. Para esto, utilizamos la función `search_tweets()` que permite obtener tweets que cumplan los parámetros que fijemos.

``` r
tweets <- search_tweets("palabra", since = "fecha", n = 30000)

tweets_hashtag <- search_tweets("Hashtag", since = "fecha", n = 30000)

tweets_hashtag <- search_tweets("elecciones+CABA", since = "fecha", n = 30000) #Trae tweets que tengas esas dos palabras en ese orden 

tweets_hashtag <- search_tweets("elecciones CABA", since = "fecha", n = 30000) #TRae todos los tweets que contengan esas dos palabras sin importar el orden en el que esten mencionados. 
```

Y por último, podemos pedirle a twitter que nos de datos en tiempo real o **streaming**. Como alternativa a consultar el archivo "histórico" de Twitter, es posible conectar a su API de streaming, que entrega tweets en tiempo real al instante en que se producen.

La función `stream_tweets()` permite iniciar una conexión y capturar tweets hasta que concluya el tiempo dispuesto por el parámetro "timeout", expresado en segundos.

``` r
captura_streaming <- stream_tweets(q = "último+momento", timeout = 60) #un minuto de escucha en tiempo real

#busqueda por un tiempo determinado que establecemos en la variable "tiempo". Por ejemplo para 3 dias de escucha 24*60*3

captura_streaming <- stream_tweets(q = terminos_de_busqueda, 
                           timeout = tiempo,
                           file_name = archivo,
                           token = mytoken)

captura_streaming <- rtweet::parse_stream("busqueda_tweets_DT_VP.json")
```

Para leer análisis con datos de twitter recomendamos el "Observatorio de redes" --&gt; <https://medium.com/@O_de_R>

Web Scrapping
-------------

#### ¿Qué es HTML? <sup>1</sup>

El **Lenguaje de Marcado de Hipertexto (HTML)** es el código que se utiliza para estructurar y desplegar una página web y sus contenidos. Por ejemplo, sus contenidos podrían ser párrafos, una lista con viñetas, o imágenes y tablas de datos.

HTML no es un lenguaje de programación; es un **lenguaje de marcado que define la estructura de tu contenido**. HTML consiste en una serie de elementos que usarás para encerrar diferentes partes del contenido para que se vean o comporten de una determinada manera.

Las *etiquetas de encierre* pueden hacer de una palabra o una imagen un hipervínculo a otro sitio, se pueden cambiar palabras a cursiva, agrandar o achicar la letra, etc. Por ejemplo, tomemos la siguiente línea de contenido:

        "Mi gato es muy gruñón" 

Si queremos especificar que se trata de un párrafo, podríamos encerrar el texto con la etiqueta de párrafo:

      <p>Mi gato es muy gruñon</p> 
      

1.  La etiqueta de apertura: consiste en el nombre del elemento (en este caso, p), encerrado por paréntesis angulares (&lt; &gt;) de apertura y cierre. Establece dónde comienza o empieza a tener efecto el elemento — en este caso, dónde es el comienzo del párrafo.

2.  La etiqueta de cierre: es igual que la etiqueta de apertura, excepto que incluye una barra de cierre (/) antes del nombre de la etiqueta. Establece dónde termina el elemento — en este caso dónde termina el párrafo.

3.  El contenido: este es el contenido del elemento, que en este caso es sólo texto.

4.  El elemento: la etiqueta de apertura, más la etiqueta de cierre, más el contenido equivale al elemento.

<sup>1</sup>Tomado de <https://developer.mozilla.org/es/>

#### Scrapeo de HTML con `rvest`

``` r
library(tidyverse) 
library(rvest) 

#Por ejemplo, tomemos la tabla de diputados nacionales 

diputados <- read_html("https://www.hcdn.gob.ar/diputados/listadip.html") 

diputados_tabla <- diputados %>% 
                  html_node("table") %>% 
                  html_table() 

knitr::kable(diputados_tabla[1:5,1:6])
```

| Foto | Diputado                          | Distrito            | Inicia mandato | Finaliza mandato | Bloque                       |
|:-----|:----------------------------------|:--------------------|:---------------|:-----------------|:-----------------------------|
| NA   | Abdala De Matarazzo, Norma Amanda | Santiago Del Estero | 10/12/2017     | 09/12/2021       | FRENTE CIVICO POR SANTIAGO   |
| NA   | Acerenza, Samanta Maria Celeste   | Buenos Aires        | 10/12/2015     | 09/12/2019       | PRO                          |
| NA   | Aicega, Juan                      | Buenos Aires        | 10/12/2017     | 09/12/2021       | PRO                          |
| NA   | Allende, Walberto Enrique         | San Juan            | 10/12/2017     | 09/12/2021       | TODOS JUNTOS POR SAN JUAN    |
| NA   | Alonso, Laura V.                  | Buenos Aires        | 10/12/2017     | 09/12/2021       | FRENTE PARA LA VICTORIA - PJ |
