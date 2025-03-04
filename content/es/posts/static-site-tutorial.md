---
title: "Algo así como un tutorial para crear sitios estáticos"
date: 2025-03-03
draft: false
---

Crear un sitio web estático debería ser fácil. Y lo es. En este post voy a mostrar cómo creé el blog donde estás leyendo esto.

<!--more-->

# Introducción

Para entender las decisiones que tomé, un buen punto de partida es conocer mis requisitos.  
Yo quería un blog que cumpliera con lo siguiente (en orden de importancia):  

1. Su costo debía ser 0.  
2. Debía ser simple de configurar y mantener.  
3. Debía ser visualmente agradable.  
4. Quería poder obtener métricas sobre mi sitio.  

# Definición de tecnologías

Si pensamos en un blog estático, probablemente lo primero que se nos venga a la cabeza sea [GitHub Pages](https://pages.github.com/). Este servicio nos permite crear y alojar sitios web estáticos de forma gratuita. Solo tienes que subir tu código a un repositorio público, activar GitHub Pages y tu sitio estará disponible en internet. Perfecto, ya cumplimos con los puntos 1 y 2.  
Pero, lamentablemente, GitHub Pages no tiene una forma de ver métricas "out of the box", como se puede ver en esta [discusión](https://github.com/orgs/community/discussions/31474). Aquí es donde entra [Cloudflare Pages](https://pages.cloudflare.com/), esta herramienta nos ofrece lo mismo y algunas cosas más de [manera gratuita](https://www.cloudflare.com/plans/developer-platform/). En particular, trae un dashboard de web analytics muy completo.  
Ahora sí cumplimos con los puntos 1, 2 y 4. ¿Y qué hay del 3? Bueno, cuando apenas comencé mi investigación, la primera herramienta que encontré para generar sitios estáticos fue [Jekyll](https://jekyllrb.com/), que es básicamente un generador de sitios estáticos que, utilizando plantillas, convierte nuestros archivos Markdown en algo bonito.  
Pero, por supuesto, no me quedé con la primera opción que encontré, así que seguí buscando y llegué a [Hugo](https://gohugo.io/), otro generador de sitios estáticos con características muy similares. Personalmente, no encontré que uno sea mucho mejor que el otro y finalmente opté por Hugo. Pueden encontrar una excelente comparación en este [post](https://draft.dev/learn/hugo-vs-jekyll).   

# Pasos para la implementación

1. **Creación de repositorio:** Podemos utilizar GitHub o GitLab, y puede ser público o privado. En mi caso, creé un [repositorio público](https://github.com/valenvilardav/blog) en GitHub donde puedes ver el código utilizado en este blog.  

2. **Creación del nuevo sitio:** Debemos utilizar el comando `hugo new site` para crear la estructura de directorios, luego instalar alguna plantilla siguiendo la documentación y finalmente pushear todo a nuestro nuevo repositorio.  

3. **Integración con Cloudflare Pages:** Para crear una nueva página, debemos ingresar a Cloudflare y en la sección de "Workers & Pages" crear una nueva aplicación. Para esto necesitaremos conectar Cloudflare con nuestra herramienta de versionado de código. En el caso de GitHub, simplemente basta con instalar una [app](https://docs.github.com/en/apps/overview) y darle permiso sobre el repositorio indicado.  

4. **Configuración de build y deployment:** Esta parte es bastante directa. Podemos utilizar un [preset](https://developers.cloudflare.com/pages/configuration/build-configuration/) para el lenguaje que estemos utilizando. En mi caso, el tema que estoy utilizando requiere instalar una dependencia con npm, así que mi comando de build es `npm install && hugo`.  

   Algo importante a tener en cuenta es setear la versión de Hugo y Node con las variables `HUGO_VERSION` y `NODE_VERSION` respectivamente, ya que si no se utilizarán versiones viejas por defecto, lo cual puede traer problemas.  

5. **Acceso al sitio:** Ya podemos ingresar a nuestra web en el dominio que nos provee Cloudflare.  

## ¿Y si quiero configurar un dominio personalizado?

Para esto debemos poder administrar nuestro dominio desde Cloudflare. En mi caso, lo compré en Hostinger, por lo que tuve que cambiar los registros NS para utilizar los de Cloudflare. Luego, simplemente debemos agregar un [dominio personalizado](https://developers.cloudflare.com/pages/configuration/custom-domains/) a nuestra página.  