---
title: Antes de comenzar
linktitle: Antes de comenzar
weight: 10
author: ''
date: '2019-08-04'
slug: antes-de-comenzar
categories:
  - Lecciones R
tags:
  - Lecciones R
lastmod: '2019-08-04T19:48:12-03:00'
layout: post
type: post
highlight: no
---

# ¿Qué es R y R Studio? 

R Studio es un _entorno de desarrollo integrado_ (iDE en su sigla en inglés) para el lenguaje de programación R. Por este motivo, para poder utilizar el RStudio debemos instalar también el R. Lo importante del lenguaje R es que es un __software libre y gratuito y de código abierto__. 

<center>
![](/posts/2019-08-04-antes-de-comenzar_files/logosR.png)
</center>

El __IDE__ permite escribir un script o código, navegar los archivos guardados en la computadura, revisar las varibales creadas, visualizar, desarrollar librerias. De esta forma, la ventaja de utilizar __R__ es que _toda_ la información que necesitamos para escribir el código, lo tenemos en una misma "ventana"

Estas condiciones han fomentado el desarrollo de una gran cantidad de usuarios y desarrolladores. Además, los usuarios de R pueden crear y corregir “bugs” de paquetes (veremos qué son a continuación). 

El aspecto más relevante de R es la __explosión de la ciencia de datos__ y la comunidad diversa de usuarios que ha podido conformar. Los cursos, manuales y sitios para consultar errores y problemas son sumamente útiles a la hora de comenzar a trabajar con este lenguaje. 


## Características de R:

__1__ Permite desarrollar _scripts sencillos_, que no necesitan grandes o complejos cambios para ser reproducidos o si cambiamos la base datos analizada

__2__ RStudio es particularmente bueno para _reproducir los análisis por distintas personas_. Esto es fundamental para copiar scripts, compartirlos para continuar el trabajo o consultar errores, etc. 

__3__ R es _interdisciplinario y extensivo_. Debido a la gran cantidad de paquetes que posee, se puede utilizar R para desarrollar _análisis estadísticos_, _análisis de textos_, _visualizaciones_, _estudios georreferenciados_, etc.

__4__ R utiliza datos de _cualquier forma y tamaño_. Lo que es fundamental si queremos fortalecer los conocimientos en Data Analysis y eventualmente trabajar con Big Data. 

__5__ R produce una gran cantidad de __gráficos__ de calidad 

__6__ R tiene una _comunidad amplia_ y en crecimiento, con meetups, encuentros y datatones. 


## ¿Cómo lo bajamos? 

Tanto R como RStudio se bajan de las siguientes páginas web:

- https://cran.r-project.org/bin/windows/base/
- https://www.rstudio.com/products/rstudio/download/

***

# Conociendo RStudio

### Los cuatro paneles
Ahora bien, ¿con qué nos encontramos al abrir RStudio? El programa está compuesto de 4 paneles fundamentales. 

<center>
![](/posts/2019-08-04-antes-de-comenzar_files/panelRstudio.png)
</center>

__Panel de edición__: es el script donde vamos a trabajar y desarrollar nuestros códigos. Es el único que no aparece al abrir el RStudio. Para crearlo debemos ir al logo del archivo con un __+ verde__. De ahí utilizaremos dos tipos de archivo: __R Script__ y __R Markdown__.

__Consola__: en este panel se realizan los comandos desarrollados en el “panel de edición”. También se puede trabajar directamente en la consola, pero nosotros no vamos a usarlo por ahora. La consola es importante para nosotros porque nos dice si hubo errores en nuestro script y suele ser muy preciso en qué nos equivocamos. Además, como veremos, sirve para preguntar sobre los paquetes y sus códigos.  

__Enviroment e Historia__: este panel cuenta con los datasets y los valores que desarrollemos en nuestro Panel de edición. 

__Cuarto panel__: este panel es muy general, cuenta con los paquetes que tenemos bajados en nuestro R, así como también nos indica los archivos que están disponibles en nuestro working directory y presenta las visualizaciones que elaboramos en nuestro panel de edición. 

### Nuevo Proyecto, Nuevo Archivo y tipos de archivos 

Podemos dividir R en dos: los __PROYECTOS__ y los __ARCHIVOS (files)__. 

+ __PROYECTO__: es fundamental, ya que nos crea una carpeta donde guardaremos todos los archivos necesarios para llevar a cabo nuestro trabajo. Es importante tener en cuenta esto: al crear un proyecto, creamos un _Working Directory_. Nos conviene remitir todos los archivos que tengamos en la computadora al WD para acceder a ellos más fácilmente. 

Para Crear un Proyecto, vamos a _FILE > New Project > New Directory > New Project_. Esto nos creará una nueva carpeta que contendrá el proyecto de R. 
Si queremos trabajar en otro tipo de proyecto, lo ideal es crear OTRO PROYECTO, en lugar de otro Archivo. 

+ __ARCHIVO (FILE)__: Para crearlo vamos a _FILE > New File > R script_ ó _FILE > New File > R Markdown_. Vamos a usar dos tipos de archivos: _R Script (el más común)_ y el _R Markdown_. 


### WORKING DIRECTORY

El _wd()_ es el lugar donde trabaja R, donde buscará y guardará los archivos. 

* Para establecer o cambiar el _wd()_ podés usar: 

```
setwd("/path/to/working/directory")
```


* Si querés chequear que estás trabajando en el _wd()_ correcto, podés usar: getwd() y devolverá el path 


```{r}
getwd()
```

# Interactuando en R 

Las bases de la programación está en escribir "guiones" para que luego, cuando le ordenemos, la computadora los lea y ejecute. Escribimos en código y mantenemos unn lenguaje común. 

Tenemos 2 fotmas de interactuar con R: 

* Usando la _consola_  > tipeamos los comando directamente en la consola y apretamos __Enter__ para ejecutarlos. #ATENCIÓN!# Lo que escribimos en la consola, se borrará al salir

* Usando el _panel de edición_ > escribimos el script y lo guardamos para poder utilizar el código en el futuro o compartirlo! Para ejecutar un script podemos hacerlo directamente usando __Ctrl + Enter__, posando el cursor sobre la linea de código. 

## Paquetes y bibliotecas

### PACKAGES (PAQUETES)

Ahora que aprendimos los aspectos básicos de RStudio, y antes de empezar a trabajar con nuestros códigos, es importante explicar qué son los __“paquetes”__ o packages. Estos son __funciones o programas__ que extienden la utilización de R. Por ejemplo, hay algunos comandos, acciones, gráficos y colores que no se encuentran instalados en RStudio. 

Installing additional packages using the packages tab

In addition to the core R installation, there are in excess of 10,000 additional packages which can be used to extend the functionality of R. Many of these have been written by R users and have been made available in central repositories, like the one hosted at CRAN, for anyone to download and install into their own R environment. In the course of this lesson we will be making use of several of these packages, such as ‘ggplot2’ and ‘dplyr’.


Para eso, debemos “descargarlos" o "instalarlos" 

Hay dos formas para adquirir los paquetes. 

* 1. FORMA MANUAL
Simplemente vamos a la ventana _PACKAGES_ del panel que se encuentra abajo a la derecha (1) y ahí vamos a _INSTALL_

En _INSTALL_ nos aparecerá la ventana Install Packages, donde anotaremos el nombre del paquete que queremos bajar. En el ejemplo, el paquete es __tidyverse__.

* 2. MEDIANTE SCRIPT
La otra forma de instalar un paquete es mediante la utilización del _script_. Simplemente copiamos lo siguiente en nuestro panel de edición y usammos el atajo de __"Ctrl + Enter"__

```{r, eval=FALSE}
install.packages("tidyverse")
```


Esta forma de instalar un paquete es más práctica y mejor si nuestra intención es compartir el script con otras personas, ya que ellas pueden copiar todo el código y correrlo, sin tener que hacer la instalación manual.  

### BIBLIOTECAS (LIBRARY)

¡Ya instalamos el paquete! ¿Podemos utilizarlo? Todavía no. La función INSTALL me trae el paquete y la guarda en mi “biblioteca”. Pero lo que debemos hacer para poder usarlo es “llamarlo”. También hay dos maneras de hacer esto.

1. FORMA MANUAL
Sencillamente, vamos al panel de PACKAGES y presionamos en el espacio del paquete que hayamos bajado (en este caso: tidyverse). Para buscarlo podemos copiar su nombre en el espacio de la lupa.

2. MEDIANTE SCRIPT
Tal como hicimos con la instalación, copiamos en el panel de edición y usammos el atajo de __"Ctrl + Enter"__

```{r warning=FALSE}
library("tidyverse")
```


De esta forma, ya podremos usar el paquete que instalamos.  

__¡Estamos listos!__
