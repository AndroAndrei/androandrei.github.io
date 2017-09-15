---
layout: post
title: 'Instalación de github-pages-Errores comunes'
date: 2017-9-15
published: true
---

### Formato de la publicación: Guía.
## Host: Linux

**INDICE**

* Introducción.
* El Problema.
* Análisis del problema.
* Solución del problema.
* Conclusión.
* Referencias


## Introducción
No es muy complicado encontrar muy buenas publicaciones(Posts) que nos presenten una guiá 
detallada de como proceder a preparar el entorno de desarrollo local de tu Blog
alojado en GitHub. En especial, aunque en ingles, esta de la reconocida [smashingmagazine](https://www.smashingmagazine.com/2014/08/build-blog-jekyll-github-pages)

Lo que muy poco se muestra, sin embargo, son algunos errores comunes que suelen suceder. Este post lo dedico
a presentar la solución a uno de estos problemas que me sucedió a mi. Esto con motivo de 
auto referencia y por si le es útil a alguien que se encuentre con esta publicación.

## El Problema
El problema que documento aquí se presenta luego de intentar instalar la gema **github-pages**.
La cual necesitamos para la correcta sincronización de las dependencias(gemas), incluyendo jekyll, del 
entorno de desarrollo (local) con sus correspondientes de producción(GitHub).

Luego de proceder con la instalación de la gema github-pages:
```bash
ruby gem install github-pages
``` 

Suele presentarse el siguiente **error**:

```bash
ERROR:  Error installing github-pages:
	ERROR: Failed to build gem native extension.
```

## Análisis del problema
Generalmente cuando instalamos ruby no se instalan las cabeceras de desarrollo
de este. Siendo este el principal causante de estos **errores comunes**.


## Solución del problema
Siendo este el caso. Lo primero que debemos hacer es instalar las cabeceras de
desarrollo de ruby:

```bash
apt-get install ruby-de
```

Algunas veces incluso al instalar estas dependencias se nos siguen presentando errores

Lo importante aquí es prestar atención a los mensajes de error que presenta el ruby, ya que,
es aquí donde podemos encontrar pistas de lo que ha salido mal. Muchas veces lo primero que 
hacemos es copiar el error y consultar en *stackoverflow* pero lamentablemente muchas veces 
no encontraremos una solución contundente si acaso alguna.

Lo primero que note en mi caso fue que no se pudo construir la librería **libxml2**. Esto debido 
a la falta de una dependencia.

```bash
zlib is missing: necessary for building libxml2
```

si ya tenemos zlib instalado en nuestro sistema(podemos comprobarlo viendo si **man zlib** nos devuelve algo)
entonces lo que nos falta seria instalar sus cabeceras de desarrollo:

```bash
sudo apt-get install zlib1g-dev
```

Si al volver a ejecutar `ruby gem install github-pages` se te presenta el siguiente error:

```bash
No such file or directory - getcwd
```

Tienes que cerrar sesión en esa terminal o abrir otra terminal.

## Conclusión
Esto es todo por el momento. Espero que os haya sido útil

## Referencias
[install ruby on rails](https://technotes.tt4living.com/ruby-on-rails/install-ruby-on-rails)  
[GitHub issue](https://github.com/github/pages-gem/issues/133)  
[smashingmagazine](https://www.smashingmagazine.com/2014/08/build-blog-jekyll-github-pages)  