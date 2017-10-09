# Markdown con Sublime Text

En este documento se describen las instrucciones para la creación de documentos usando Markdown, Sublime Text y Pandoc.

# Instalación

## Sublime Text

Mi herramienta preferida para trabajar con Markdown es [Sublime Text](http://www.sublimetext.com). Tradicionalmente he usado la versión 2 pero actualmente ya está disponible la versión 3 (que ha estado en Beta durante muchos años).

### Temas y paquetes

Una vez instalada es recomendable instalar varios paquetes que nos ayudarán a preparar el entorno de trabajo. Aunque no sean todos para Markdown, los paquetes que tengo instalados son:

- `Package Control`. Sirve para poder instalar otros plugins de Sublime más adelante. [En la versión 2 este paquete se instala a mano siguiendo las instrucciones que aparecen aquí.](https://packagecontrol.io/installation). En la versión 3 existe ya una opción para instalar Package Control desde el propio editor (`Shift+Cmd+P` (Mac) o `Shift+Ctrl+P` (Windows) >> Install)
- `Markdown Editing` a través del _Package Control_:
    + `Shift+Cmd+P` (Mac) o `Shift+Ctrl+P` (Windows) >> Package Control - Install package >> Markdown editing
- `AdvancedNewFile`
- `Alignment`
- `Clickable URLs`
- `Docblockr`
- `Emmet`
- `Gist`
- `HTML-CSS-JS Prettify`
- `JSHint`
- `Terminal`
- `Sublime Git`
- `Sidebar Enhancement`
- `Pretty JSON`
- `Pandown`: Se explica en detalle más adelante ya que es fundamental para la exportación de Markdown.

A veces la instalación de `Package Control` no funciona a la primera. Es probable que haya que instalar/desintalar alguna vez hasta que funcione correctamente.

## Pandoc

[PanDoc](http://pandoc.org) es el responsable de hacer la conversión de Markdown a múltiples formatos. Una vez que se ha instalado (siguiendo [estas instrucciones de instalación](http://pandoc.org/installing.html)) hay que tener en cuenta que en cada sistema operativo se instala por defecto en un lugar distinto (y es necesario conocerlo para configurar Pandown):

- En Windows, Pandoc se instala en `C:\\Users\\MIUSUARIO\\AppData\\Local\\Pandoc` o en `c:\\Archivos de programa (x86)\\Pandoc`. 
- En MacOSX, Pandoc se instala un enlace simbólico en `/usr/local/bin`. Si seguimos el enlace veremos que el original queda instalado en `/usr/local/Cellar/pandoc/<VERSION>/bin`
- En MacOSX también se puede instalar con Homebrew `brew install pandoc`

> Nota: las carpeta `AppData` y `.pandoc` son directorios ocultos del sistema Windows y Mac, respectivamente.

## Pandown

El paquete `Pandown` es el responsable de hacer la conversión de markdown a otros formatos usando pandoc. Para instalarlo usaremos _Package Control_.

- `Shift+Cmd+P` (Mac) o `Shift+Ctrl+P` (Windows) >> Package Control - Install package >> Pandown

En caso de instalarlo en Windows es necesario configurar dónde se encuentra Pandoc (en Linux y Mac suele quedar correctamente configurado por defecto):

- Preferences >> Package Settings >> Pandown >> Settings - Default
- En el archivo de preferencias globales que se abre, sustituir el valor de `install_path` (por defecto es `/usr/local/bin`) por la ruta en la que se ha instalado Pandoc (recordar que hay que poner dobles barras `\\` en la ruta)
- Si no nos deja editar el archivo de preferencias globales (ocurre con Sublime Text 3), entonces tendremos que:
    - Abrir el archivo de preferencias del usuario (Preferences >> Package Settings >> Pandown >> Settings - User)
    - Copiar y pegar el de preferencias globales (el que se vio en el paso anterior)
    - Modificar el valor de (por defecto es `/usr/local/bin`) por la ruta en la que se ha instalado Pandoc (recordar que hay que poner dobles barras `\\` en la ruta)

Una vez que está todo instalado ya podemos escribir el texto en Markdown. En particular se puede usar la versión de Markdown que utiliza Pandoc y que explicaremos más en detalle en la [siguiente sección](#mdpandoc).

Con `Shift+Cmd+P` (Mac) o `Shift+Ctrl+P` (Windows) podemos compilar nuestro documento en Markdown a distintos formatos como PDF (a través de Latex), Beamer o pases de dispositivas en HTML como Slidy, DZSlides (las más chulas) S5 o Slidious. Escribiendo la palabra `pandown` veremos que aparecen todos los posibles formatos de conversión. Si no funciona correctamente entonces es necesario que el Build System activo sea `Pandown MarkDown` (menú Tools >> BuildSystem).


Para saber más acerca de cómo crear transparencias usando Pandoc podemos [leer la siguiente sección del manual  de Pandoc](http://johnmacfarlane.net/pandoc/README.html#producing-slide-shows-with-pandoc)

# Sintaxis básica de Markdown

Markdown es un lenguaje mínimo de marcas. Existen variaciones de esta sintaxis aunque, salvo por pequeñas sutilezas, todas terminan siendo similares. Por ejemplo, [GitHub Flavored Markdow (GFM)](https://github.github.com/gfm/) es la sintaxis usada en GitHub y que permite que podamos ver renderizado en HTML cualquier documento en Markdown (extensión md) que subamos a GitHub.

A continuación vamos a detallar las principales marcas que solemos utilizar de entre [todas que ofrece el Markdown que Pandoc es capaz de interpretar](http://pandoc.org/MANUAL.html#pandocs-markdown).

## Párrafos

Un párrafo es una o más líneas de texto _seguido de una o varias líneas en blanco_. 

## Énfasis simple

Cualquier palabra o texto entre `_` o `*` quedará enfatizado (generalmente _en cursiva_). Si ponemos dos `__` o dos `**` lo pondremos en **negrita**.

## Encabezados

Se escriben poniendo tantos símbolos `#` como nivel de encabezado que queramos poner (estilo ATX) o subrayando el texto de la Encabezado con símbolos `=` o `-`. Por ejemplo:

    Encabezados
    ---------

y 

    # Encabezados

Generan el código `<h1>Encabezados</h1>`, en HTML, o un párrafo con estilo Título 1, en Word (dependiendo de a qué formato los convirtamos). 

Los encabezados pueden incluir un identificador añadiendo `{#nombreId}` al final del encabezado. De esta forma se pueden hacer [referencias cruzadas](#enlaces-y-referencias-cruzadas). También pueden tener otros atributos como `{.unnumbered}` o `{-}`, que hace que esa Encabezado no esté numerada.

## Enlaces y referencias cruzadas 

Hay varias formas de añadir enlaces:
 
- __Enlaces inline__: El texto del enlace y a dónde nos lleva está todo junto. El texto o título del enlace se pone entre `[]` y la dirección del enlace se pone a continuación entre `()`. En la dirección se puede poner el identificador de un encabezado para hacer una _referencia cruzada_. Por ejemplo, [este enlace a la página web de Google](http://www.google.es) se ha creado escribiendo:

```
[este enlace a la página web de Google](http://www.google.es)
```

> Si hemos instalado `Markdown Editing` en Sublime entonces podemos crear rápidamente este tipo enlace escribiendo `mdl` y pulsando la tecla `Tab`.


-  Si no queremos poner texto de un enlace entonces podemos poner una dirección entre `<>`. Por ejemplo, este enlace <http://google.com> se ha escrito como `<http://google.com>`.

- __Enlaces referencia__: El texto del enlace y a dónde nos lleva se escriben en diferente lugar, de modo que el texto que estamos escribiendo queda más claro. El texto o título del enlace se pone entre `[]` y, a continuación, se pone el texto de una etiqueta entre `[]`. Si no se pone el texto de la etiqueta entonces el texto del enlace hace las veces de etiqueta. La definición del enlace en sí misma puede aparecer en cualquier otro lugar del texto y consiste en `[idLabel]: URL "título"` donde el título es el título del enlace, puede ir entre `""` o `()` y es opcional. Por ejemplo, podemos [poner un enlace a PanDoc][PanDoc] escribiendo `[poner un enlace a PanDoc][PanDoc]`. El enlace en sí lo hemos definido un poco más adelante con el siguiente código:
 
 ```
 [PanDoc]: http://johnmacfarlane.net/pandoc/
 ```


[PanDoc]: http://johnmacfarlane.net/pandoc/


## Imágenes

Son links precedidos del caracter `!`. El texto entre `[]` hace las veces de pie de figura. Si el enlace termina en `\` entonces significa que la imagen es inline dentro del párrafo en la que está escrita.

Por ejemplo `![Pie de figura: Imagen](./img/imagen.png)` hace que salga lo siguiente:

![Pie de figura: Imagen](./img/imagen.png)

> Si hemos instalado `Markdown Editing` en Sublime entonces podemos crear rápidamente este tipo enlace escribiendo `mdi` y pulsando la tecla `Tab`.


## Enumeraciones y viñetas

Una lista con balas consiste en una serie de párrafos que empiezan con `*`. Por ejemplo, el texto:

```
* Un
* Dos
* Tres
```

Se convierte en

* Un
* Dos
* Tres

Se puede añadir un nuevo nivel precediendo cada línea por un tabulador o 4 espacios en blanco. Aunque el símbolo a usar puede ser el mismo (`*`) Por legibilidad se pueden usar otros símbolos (como `+` o `-`). Por ejemplo, el texto:

    * Uno
    * Uno.Uno
    * Uno.Dos
        * Uno.Dos.Uno


Se convierte en:

* Uno
    * Uno.Uno
    * Uno.Dos
        * Uno.Dos.Uno

Si queremos poner texto indentado con respecto a una viñeta entonces tendremos que dejar una línea en blanco tras la línea de la viñeta y, a continuación, escribir el párrafo comenzando por un tabulador o 4 espacios en blanco.

```
* Palabra

    Definición de la palabra
```

* Palabra

    Definición de la palabra

Las listas ordenadas comienzan por números, en lugar de símbolos. Los números que se pongan son ignorados por lo que la lista:

    1. Uno
    4. Dos
    5. Tres

Sirve para crear la lista enumerada

1. Uno
4. Dos
5. Tres

Podemos hacer que una lista enumerada continúe con la numeración después de poner algunos párrafos entre medias usando para numerarlos el símbolo `(@)`.

Si queremos que el siguiente texto indentado o de una lista no se considere como de la primera lista entonces tendremos que añadir un párrafo no indentado. Lo más habitual es poner un comentario HTML como `<!-- Fin de lista -->`

Por último, se pueden crear listas de definiciones (tienen sus propias marcas en HTML). Para hacerlo escribimos el nombre del término a definir y, dos párrafos después, escribimos la definición comenzando por `:` o `~`. Por ejemplo:

    Palabra 1

    :   Lorem ipsum dolor sit amet, consectetur adipisicing elit. Reiciendis, ullam, ut, odio, voluptates illum placeat tempora iste numquam delectus voluptas excepturi rem dolorum omnis obcaecati ratione sequi voluptatem earum voluptate.

    Palabra 2 (con **formato**)

    ~   Lorem ipsum dolor sit amet, consectetur adipisicing elit. Laborum, ut, recusandae, quam, aliquid dolores sapiente eveniet dolorem ipsam voluptatibus tempore doloribus voluptatum? Fugit, repudiandae ad mollitia amet temporibus animi quo.


Se convierte en:

Palabra 1

:   Lorem ipsum dolor sit amet, consectetur adipisicing elit. Reiciendis, ullam, ut, odio, voluptates illum placeat tempora iste numquam delectus voluptas excepturi rem dolorum omnis obcaecati ratione sequi voluptatem earum voluptate.

Palabra 2 (con **formato**)

~   Lorem ipsum dolor sit amet, consectetur adipisicing elit. Laborum, ut, recusandae, quam, aliquid dolores sapiente eveniet dolorem ipsam voluptatibus tempore doloribus voluptatum? Fugit, repudiandae ad mollitia amet temporibus animi quo.

## Citas y código

Cualquier párrafo que comienza con el caracter `>` se considera un bloque de cita (o 'quote'). Los bloques de citas se pueden anidar unos dentro de otros separando el siguiente bloque con un espacio en blanco y el símbolo `>`.

Los bloques de código (_verbatim_) son aquéllos que están indentados con un tabulador o 4 espacios en blanco. También se considera verbatim a todo aquello que haya entre dos líneas de al menos 3 `~` (virgulillas) o 3 ` ` ` (tildes). Como en:

    ~~~~~~~
    if (a > 3) {
      moveShip(5 * gravity, DOWN);
    }
    ~~~~~~~
 
que se convierte en

~~~~~~~
if (a > 3) {
  moveShip(5 * gravity, DOWN);
}
~~~~~~~

Detrás de la primera línea de virgulillas o tildes podemos añadir el nombre del lenguaje del código para que lo coloree de acuerdo a la sintaxis de ese lenguaje. Alternativamente, podemos poner un identificador para crear una referencia cruzada al código escribiéndolo entre `{ }` tras la línea de virgulillas o tildes.

> Si hemos instalado `Markdown Editing` en Sublime entonces podemos crear rápidamente este tipo enlace escribiendo `mdc` y pulsando la tecla `Tab`.

## Notas al pie

Existen dos tipos de formato:

- Formato corto: Basta con poner `[^1]`. Luego pondremos el contenido de esa nota tal y como lo hicimos con las [referencias cruzadas](#refCruz) de la siguiente forma.

~~~
    [^1]: Contenido de la nota.
~~~

- Formato largo: Se utiliza cuando la nota ocupa varios párrafos. En este caso el enlace se caracteriza por poner un identificador: `[^identificador]`. Al igual que antes, usaremos las referencias cruzadas para poner el contenido de la nota.

## Algunos metadatos y caracteres de escape

Los documentos pueden contener ciertos metadatos que ayudan a algunos conversores a añadir información adicional. Por ejemplo, el bloque de título se define de la siguiente manera:

    % Título
    % Autores (separados por comas)
    % Fecha

Si lo convertimos a Beamer, por ejemplo, veremos que se convierte en la primera diapositiva de presentación. En HTML se convierte en el título de la página.

También podemos poner metadatos en formato YAML, preferiblemente al principio del documento. Se escribe entre `---`, tal y como se puede ver en este ejemplo:

```
---
title: Sublime y Markdown
section: 2
next: 3-markdown
prev: 1-intro
---
```

Los metadatos que aparecen pueden ser utilizados por pandoc para producir cierta información en los documentos generados en la conversión. Por ejemplo, los metadatos anteriores pueden ser usados (con la plantilla adecuada) para crear un HTML con el título indicado en `title`, un encabezado con el número de la sección (`section`) y unos enlaces de navegación que nos llevan al documento anterior (`prev`) y siguiente (`next`).

Los símbolos de escape llevan delante el símbolo `\`. Se pueden "escapar" los siguientes símbolos:

```
\`*_{}[]()>#+-.!
```

## Tablas

Markdown permite también crear tablas de manera sencilla. Como generalmente no las uso [dejo aquí el enlace con la sintaxis detallada de las tablas](http://pandoc.org/MANUAL.html#tables). 

# Exportación con Pandown

Pandoc es [una aplicación de consola](https://pandoc.org/MANUAL.html) que permite, entre otros, convertir un documento en Markdown a otros tipos de documentos (como HTML, LaTeX, PDF, DOCX...). Sin embargo, una forma más cómoda de usarlo es mediante Pandown, el plugin de Sublime.

Podemos probar que la exportación con este plugin funciona abriendo un documento en Markdown y realizando lo siguiente:

> `Shift+Cmd+P` (Mac) o `Shift+Ctrl+P` (Windows) >> Build: Pandown HTML 5

Una vez ejecutado esto, en el directorio en el que se encuentra el documento en Markdown debería de aparecer un documento en HTML equivalente. 

Como se habrá podido ver al lanzar la instrucción de `build`, existen una gran cantidad de tipos de documentos a los que se puede convertir un documento en Markdown. El formato de cada uno de los tipos de documentos se define a partir de plantillas. Para tener un cierto control sobre este formato las plantillas contienen variables cuyos valores pueden ser asignados desde [los bloques de metadatos en formato YAML](#algunos-metadatos-y-caracteres-de-escape) o desde los archivos de configuración de proyectos de Pandown, que se verán a continuación. 

Podemos tener múltiples plantillas para el mismo tipo de documentos. Tan solo hay que saber cuál se usará en cada momento. Utilizando Pandown desde Sublime Text, el orden es el siguiente:

1. Si hay un **archivo de configuración de proyecto**, entonces se usarán las plantillas que se indiquen en este archivo.
2. Si no hay archivo de configuración de proyecto o dicho archivo no indica que se usen otras plantillas, entonces se usarán las **plantillas del usuario**de Pandoc.
3. Si no existen las plantillas de usuario entonces se utilizarán las **plantillas globales** de Pandoc.

Vamos a ver un poco en detalle dónde están cada una de estas plantillas y archivos.

## Plantillas globales

Las plantillas globales de Pandoc están en distinto lugar dependiendo del sistema operativo:

- **Windows**: En las últimas versiones las plantillas están incrustadas en el ejecutable. Sin embargo, se puede acceder a ellas con el siguiente comando:

```
pandoc -D *FORMATO*
```

- **Mac**: Si se ha instalado con Homebrew, las plantillas están en:

```
/usr/local/Cellar/pandoc/1.19.2.1/share/x86_64-osx-ghc-8.0.2/pandoc-1.19.2.1/data/templates
```

## Plantillas del usuario

Por defecto, no existen plantillas del usuario por lo que es necesario crearlas. Lo más sencillos es utilizar [las plantillas del repositorio de GitHub de John MacFarlane](https://github.com/jgm/pandoc-templates). Las plantillas de usuario hay que guardarlas en:

- **Windows** `c:\Users\USERNAME\AppData\Roaming\Pandoc\templates`
- **Mac** `~/.pandoc/templates`

Hay mucha gente que [contribuye compartiendo sus propias plantillas personalizadas](https://github.com/jgm/pandoc/wiki/User-contributed-templates). Por ejemplo, [hay una bastante interesante para hacer la tesis en Markdown](https://github.com/chiakaivalya/thesis-markdown-pandoc), aunque la conversión de formato no se puede hacer desde Pandown sino que hay que ejecutarla desde consola con Pandoc (hay un ejemplo completo en el repositorio).

## Archivo de configuración de proyecto

Si estamos usando Pandown y Sublime Text podemos configurar la forma en la que se ejecuta pandoc gracias al archivo de configuración de proyecto, un archivo en formato JSON en el que podemos establecer cómo queremos que se ejecute pandoc. Generalmente solemos tener un único archivo de configuración de proyecto para un conjunto de archivos en Markdown. Sin embargo, podemos utilizar múltiples archivos que se ejecutarán dependiendo de cómo hayamos abierto el proyecto en Sublime Text y en qué directorio está el archivo de configuración con respecto al archivo en Markdown que queremos convertir. A modo de ejemplo, podemos tener organizado un curso completo con distintos archivos Markdown para transparencias y apuntes y que los primeros se conviertan a transparencias con Slidy mientras que los segundos se conviertan a PDF. La organización podría ser algo similar a esto:

```
raiz
 |____ imagenes (comunes a los apuntes y presentaciones)
 |____ apuntes
 |      |____ tema01.md
 |      ...
 |      |____ pandoc-config.json (convierte a PDF)
 |____ slides
 |      |____ tema01.md
 |      ...
 |      |____ pandoc-config.json (convierte a Slidy)
 |____ ejercicios
 |      |____ ejTema01.md
 |      ...
 |      
 |____ pandownTemplates
 |      |____ slidy (libreria local y CSS personalizadas)
 |      |____ mathjax (librería local para renderizar formulas LaTeX en HTML)
 |      |____ templates
 |             |____ default.slidy
 |             |____ default.latex
 |             |____ default.opendocument
 |____ pandoc-config.json (Genérico para todo el proyecto)
```

Para indicar qué plantillas usar se puede modificar el archivo de configuración de proyecto siguiendo una de estas dos opciones:

- Buscar el campo `template` y poner como valor la ruta al archivo que se va a usar como plantilla. Esto hace que pandoc ignorará el tipo de documento y que siempre hará la conversión con la misma plantilla. A modo de ejemplo, en la organización de ficheros anterior, en pandoc-config.json del directorio de `apuntes` puede tener el valor `../pandownTemplates/templates/default.latex`, de modo que siempre genere un PDF, mientras que el del directorio de `slides` puede tener el valor `../pandownTemplates/templates/default.slidy`.
- Buscar el campo `data-dir` y poner como valor la ruta al directorio de plantillas para este proyecto. En el propio archivo de configuración se explica cuál es la estructura que ha de tener dicho directorio . Si se usa una ruta relativa, esta ha de ser con respecto al archivo Markdown que se quiere convertir. A modo de ejemplo, en la organización de ficheros anterior, podríamos poner la ruta `../PandownTemplates` como valor del campo `data-dir` en el archivo de configuración que hay en el directorio `raiz`. Con esta alternativa podríamos tener un único archivo de configuración en el raíz que indica dónde están todas las plantillas con los distintos formatos que nos interesan.

Hay que tener en cuenta que abrir un archivo individualmente en Sublime o abrir un directorio completo afecta al comportamiento de búsqueda de los archivos de configuración de proyecto en Pandown. Pandown busca primero el archivo de configuración en el directorio de trabajo del archivo que queremos convertir, para luego subir por la jerarquía de directorios _que tengamos abierta en Sublime_. Si no lo encuentra entonces utilizará pandoc normalmente, de modo que usará las plantillas de usuario o las globales, según corresponda. 

Por ejemplo, supongamos que abrimos en Sublime Text el directorio `raiz`. Si abro en el editor el archivo del `slides/tema01.md` y ejecuto Pandown siempre va a generar un archivo que usa la plantilla `default.slidy` (aunque la extensión del archivo sea otra distinta) ya que el directorio `slides` tiene su propio archivo de configuración. Por otro lado, si abro en el editor el archivo `ejercicios/ejTema01.md` y ejecuto Pandown para convertir a PDF, Slidy u OpenDocument, usará las plantillas que hay en `pandownTemplates`, ya que usará el archivo de configuración que hay en el raíz. Para cualquier otro formato usará las plantillas de usuario o globales.

Sin embargo, si en Sublime abrimos el directorio `ejercicios` (en lugar del `raiz`) y ejecutamos Pandown para convertir a PDF, Slidy u OpenDocument, en este caso se utilizarán las plantillas de usuario o las globales, ya Pandown no encontrará ningún fichero de configuración de proyecto.





