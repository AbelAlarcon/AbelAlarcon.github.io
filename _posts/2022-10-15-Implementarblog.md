---
title: Blog personal con Jekyll y GitHub Pages
date: 2022-10-15 12:00:00 +/-0800
categories: [Turorial, WEB]
tags: [jekyll, github pages]
---
# Introducción
Llevaba bastante tiempo queriendo jugar con lo necesario para levantar una página web pequeña, sí bien tengo algunas nociones básicas de HTML y CSS, llegar a un diseño que no produzca aversión y lidiar con lo necesario para hostearla, sería ese tipo *side quests* tediosas que solo completas con el objetivo de decir simplemente "lo hice". Para hacerlo más entretenido, conocer diferentes tecnologías, procedimientos y concentrarme un poco más en el contenido, probé la mezcla de Jekyll, GitHub Pages y junto a la configuración del dominio personalizado obtuve el resultado donde estas leyendo esto, así que si te interesa tener algo parecido y en una de esas aprender algo, siga leyendo compadre.

# Jekyll
Jekyll es un generador de páginas web estáticas escrito en el lenguaje de programación Ruby bajo la licencia de software MIT por uno de los co-fundadores de GitHub.

Dicho de forma rápida y simple, una página web estática cumple con entregar contenido fijo en base a sus archivos y normalmente muestra la misma información para todo usuario, un ejemplo de esto puede ser el sitio de donde se publica la [documentación de Linux](https://docs.kernel.org/). Por contraparte un sitio web dinámico se conecta a un backend y/o base de datos para generar una aplicación más interactiva con el usuario, como por ejemplo [Facebook](https://www.facebook.com/).

> Si te interesa conocer las alternativas dentro de este mundito de los generadores de sitios, puedes visitar este [enlace](https://jamstack.org/generators/).
{: .prompt-info }

## Instalación
Como se dijo, Jekyll está escrito con Ruby, particularmente se trata de una Ruby Gem, por lo que para utilizarla necesitamos primero instalar Ruby, RubyGems además de herramientas de compilación como GCC y Make. El siguiente código sirve para cualquier distribución basada en Debian.

```shell
# Instalación de los requisitos
sudo apt-get install ruby-full build-essential zlib1g-dev 
```
```shell
# Configuración de las variables de entorno
echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```
```shell
# Instalaciíon de Jekyll y Bundler
gem install jekyll bundler
```
> En caso de usar otra shell por defecto, como por ejemplo **zsh**, **ksh**, etc. usar el dotfile correspondiente.
{: .prompt-warning }

## Primeros pasos en Jekyll
Para levantar nuestro primer sitio en local con plantilla por defecto, ejecutemos lo siguiente en nuestro directorio de trabajo.

```shell
jekyll new myblog
cd myblog
bundle add webrick
bundle exec jekyll serve
```
Si todo ha ido bien, procedamos a ingresar en algún navegador a [http://localhost:4000](http://localhost:4000)

![Wellcome to Jekyll](/assets/img/Implementarblog/01_WellcomeToJekyll.png)
_Primer sitio con el tema por defecto_

Para modificar el post "Welcome to Jekyll" basta con editar el archivo en `./_post/`{: .filepath} o bien crear uno nuevo en ese lugar nombrándolo con el formato ```YEAR-MONTH-DAY-title.MARKUP```, por ejemplo ```2022-10-13-MiPrimerPost.md```

```md
---
layout: post
title:  "Este es mi primer post!"
---

# ¡Por algo se empieza!

**Hola mundo**

Aquí puedes escribir lo que quieras aunque te recomiendo mirar un poquito de Markdown para organizar mejor tu texto ^-^

```
Una vez tienes escritos tus posts o alguna modificación al código, vuelve a levantar el sitio con ```bundle exec jekyll serve``` para ver los cambios.

![My first post .md in Jekyll](/assets/img/Implementarblog/02_FirstPost.png)
_Primera publicación en local_


> Si quieres conocer más a detalle cómo crear un post, puedes visitar la documentación oficial, en especial este [enlace](https://jekyllrb.com/docs/posts/)
{: .prompt-info }

# GitHub Pages
GitHub Pages viene a ser un servicio de hosting de sitios web estáticos, principalmente usado para generar documentación y/o presentación de algún proyecto de software. La particularidad es que toma directamente los archivos HTML, CSS y JavaScript necesarios desde un repositorio y los publica por defecto bajo el dominio ```github.io```, cuyo subdominio en particular viene dado por el nombre de usuario propietario del repositorio en GitHub.

## Primeros pasos con GitHub Pages
Levantemos un sitio básico de la manera más sencilla posible. Lo primero es crear un repositorio público y nombrarlo ```UserName.github.io``` donde el ```UserName``` corresponde a tu usuario de GitHub.

![First GitHub Repository](/assets/img/Implementarblog/03_FirstRepoGitHubPages.png)
_Creación de un repositorio para GitHub Pages_

En este punto lo ideal sería saber un poco de Git y gestionar el repositorio de forma local desde una terminal, pero para efectos del ejemplo limitémonos a crear un archivo desde el navegador.

![GitHub Quick setup, creating a new file](/assets/img/Implementarblog/04_QuickSetupRepo.png)
_Cómo crear un archivo desde el quick setup_

Lo importante aquí es que el archivo creado tenga el nombre de index.html para que GitHub lo reconozca como el archivo principal a mostrar.

![Creating an HTML file](/assets/img/Implementarblog/05_IndexHTMLGHP.png)
_Archivo index.html_

Ahora solo basta esperar unos minutos y GitHub reconocerá el archivo index.html creado y mostrará su contenido al visitar la url correspondiente, en mi caso [https://abeludec.github.io](https://abeludec.github.io).

![My first Website in GitHub Pages](/assets/img/Implementarblog/06_FirstWebSite.png)
_Un "Hola Mundo" en GitHub Pages_

# Implementación
Las secciones anteriores dan una cierta idea de las dos cosas por separado, aquí se pretende mostrar de manera resumida la implementación de las dos tecnologías.

Lo primero es elegir el diseño de preferencia, para ello existe una [sección](https://jekyllrb.com/docs/themes/) en la documentación de Jekyll que recopila sitios demo con temas creados por usuarios, ahí se puede encontrar un montón de diseños, por ejemplo, desde orientados a ser un portafolio como [Neumorphism](https://longpdo.github.io/neumorphism/) hasta diseños como [LatexJekyll](http://jekyllthemes.org/themes/LatexJekyll/) con apariencia de documento LaTex.

Como elección personal se escogió el tema [Chirpy](https://chirpy.cotes.page/), las instrucciones más detalladas están en su documentación, pero básicamente es realizar lo siguiente:

1. Crear un repositorio en base al template [Chirpy Starter](https://github.com/cotes2020/chirpy-starter/generate)
![Using Chirpy Templete](/assets/img/Implementarblog/07_ChirpyTemplate.png)
_Generando el repositorio con Chirpy Starter_

2. Clonar el repositorio a tu máquina local.
```shell
git clone git@github.com:abeludec/abeludec.github.io.git
```
3. Instalar las dependencias del proyecto.
```shell
# Ejecutar el el direcorio del proyecto. Bundle: Ruby Dependency Management
bundle
```
![Chirpy dependencies](/assets/img/Implementarblog/08_RubyDependencies.png)
_Instalación de las dependencias del proyecto_
4. Editar el archivo `./_config.yml`{: .filepath} para la primera configuración.
```yml
# El archivo _config.yml viene bien comentado por lo que es sencillo ubicar que cosas cambiar.
# A continuación dejo algunas línas básicas que interea modificar.
lang: es-ES # Cambiar el idioma completo del sitio.
timezone: America/Santiago # Zona horaria para el manejo del horario en los posts.
title: Abel Alarcón # El título principal de la página
tagline: Una especie de blog (?)   # Subtitulo
url: 'https://abeludec.github.io' # Usar la url correspondiente a tu sitio
github:
  username: abelalarcon # Usuario de GitHub 
avatar: # Aquí va la ruta de la imagen de perfil del blog.
```
5. Realizar un push al repositorio con los cambios, esto desencadenará un proceso CI/CD en GitHub Action.
```shell
git add .
git commit -m "Primer test"
git push
```
![GitHub Actions Chirpy](/assets/img/Implementarblog/09_GitHubActions.png)


6. Esperar unos minutos y visitar el sitio [https://UserName.github.io](https://UserName.github.io)

De aquí en adelante solo basta con crear los posts que quieras en el directorio `./_post/`{: .filepath} y desencadenar el deploy con un push al repositorio.

> Para más información acerca de la creación de un post, visitar este [enlace](https://chirpy.cotes.page/posts/write-a-new-post/).
{: .prompt-info}

## Dominio personalizado
En caso de querer tener un dominio personalizado necesitas comprarlo en algún proveedor o bien buscar alguna alternativa gratis. En mi caso al tratarse de un **.cl**, el trámite tiene que realizarse con el Registro de Nombres de Dominio .CL [NIC Chile](https://nic.cl/). Posteriormente necesitas configurar el DNS, para eso basta con crear un registro CNAME con el subdominio que quieras a [https://UserName.github.io](https://UserName.github.io) y finalmente habilitar escribir tu dominio personalizado en la configuración del repositorio.

![Registro CNAME](/assets/img/Implementarblog/10_CNAME.png)
_Registro CNAME_
![Dominio personalizado GitHub Pages](/assets/img/Implementarblog/11_CustomDomain.png)
_Dominio personalizado GitHub Pages_


# Referencias

1. [Jekyll](https://jekyllrb.com/)
2. [GitHub Pages Documentation](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/about-github-pages-and-jekyll)
3. [Jamstack](https://jamstack.org/generators/)
4. [Marvin López - Openwebinars](https://openwebinars.net/blog/paginas-web-estaticas-vs-paginas-web-dinamicas/)
5. [Victor Cuervo - Arquitectoit](https://www.arquitectoit.com/jekyll/que-es-jekyll/)
6. [codigofacilito - Youtube](https://www.youtube.com/watch?v=GbqnwmVvp8c)
7. [Techno Tim - Youtube](https://www.youtube.com/watch?v=F8iOU1ci19Q)
8. [Javier Helguera - Youtube](https://www.youtube.com/watch?v=HVLl8GaduPQ)

