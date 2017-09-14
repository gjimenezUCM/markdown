# Markdown con Sublime Text

En este documento se describen las instrucciones para la creación de documentos usando Markdown, Sublime Text y Pandoc.

# Instalación

## Sublime Text

Mi herramienta preferida para trabajar con Markdown es [Sublime Text](http://www.sublimetext.com). Tradicionalmente he usado la versión 2 pero actualmente ya está disponible la versión 3 (que ha estado en Beta durante muchos años). Una vez instalada es recomendable instalar varios paquetes que nos ayudarán a preparar el entorno de trabajo:

- Instalar `Package Control` en Sublime. Sirve para poder instalar otros plugins de Sublime más adelante. [En la versión 2 este paquete se instala a mano siguiendo las instrucciones que aparecen aquí.](https://packagecontrol.io/installation). En la versión 3 existe ya una opción para instalar este paquete desde el propio editor.
- Instalar el paquete `Markdown Editing` a través del _Package Control_:
    + `Shift+Cmd+P` (Mac) o `Shift+Ctrl+P` (Windows) >> Package Control - Install package >> Markdown editing

A veces la instalación de `Package Control` no funciona a la primera. Es probable que haya que instalar/desintalar alguna vez hasta que funcione correctamente.

## Pandoc

[PanDoc](http://pandoc.org) es el responsable de hacer la conversión de Markdown a múltiples formatos. Una vez que se ha instalado (siguiendo [estas instrucciones de instalación](http://pandoc.org/installing.html)) hay que tener en cuenta que en cada sistema operativo se instala por defecto en un lugar distinto (y es necesario conocerlo para configurar Pandown):

- En Windows, Pandoc se instala en `C:\\Users\\MIUSUARIO\\AppData\\Local\\Pandoc` o en `c:\\Archivos de programa (x86)\\Pandoc`. 
- En MacOSX, Pandoc se instala un enlace simbólico en `/usr/local/bin`. Si seguimos el enlace veremos que el original queda instalado en `/usr/local/Cellar/pandoc/<VERSION>/bin`

>> Nota: las carpeta `AppData` y `.pandoc` son directorios ocultos del sistema.

## Pandown

El paquete `Pandown` es el responsable de hacer la conversión de markdown a otros formatos usando pandoc. Para instalarlo usaremos _Package Control_.

- `Shift+Cmd+P` (Mac) o `Shift+Ctrl+P` (Windows) >> Package Control - Install package >> Pandown

En caso de instalarlo en Windows es necesario configurar dónde se encuentra Pandoc (en Linux y Mac queda correctamente configurado por defecto):

- Preferences >> Package Settings >> Pandown >> Settings - Default
- En el archivo que se abre sustituir el valor de `install_path` (por defecto es `/usr/local/bin`) por la ruta en la que se ha instalado Pandoc (recordar que hay que poner dobles barras `\\` en la ruta)
- Si no nos deja editar el archivo (ocurre con Sublime Text 3), entonces tendremos que editar el archivo Preferences >> Package Settings >> Pandown >> Settings - User y añadir lo siguiente:

```
{
    "install_path": "<RUTA A PANDOC>"
}
```

Una vez que está todo instalado ya podemos escribir el texto en Markdown. En particular se puede usar la versión de Markdown que utiliza Pandoc y que explicaremos más en detalle en la [siguiente sección](#mdpandoc).

Con `Shift+Cmd+P` (Mac) o `Shift+Ctrl+P` (Windows) podemos compilar nuestro documento en Markdown a distintos formatos como PDF (a través de Latex), Beamer o pases de dispositivas en HTML como Slidy, DZSlides (las más chulas) S5 o Slidious. Escribiendo la palabra `pandown` veremos que aparecen todos los posibles formatos de conversión. Si no funciona correctamente entonces es necesario que el Build System activo sea `Pandown MarkDown` (menú Tools >> BuildSystem).


Para saber más acerca de cómo crear transparencias usando Pandoc podemos [leer la siguiente sección del manual  de Pandoc](http://johnmacfarlane.net/pandoc/README.html#producing-slide-shows-with-pandoc)

# Principal sintaxis de Markdown

Markdown es un lenguaje mínimo de marcas. A continuación vamos a detallar las principales marcas usadas de entre [todas que ofrece el Markdown que Pandoc es capaz de interpretar](http://pandoc.org/MANUAL.html#pandocs-markdown).

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

Los encabezados pueden incluir un identificador añadiendo `{#nombreId}` al final del encabezado. De esta forma se pueden hacer [referencias cruzadas](#refCruz). También pueden tener otros atributos como `{.unnumbered}` o `{-}`, que hace que esa Encabezado no esté numerada.

## Enlaces y referencias cruzadas {#refCruz}

Hay varias formas de añadir enlaces:
 
- __Enlaces inline__: El texto del enlace y a dónde nos lleva está todo junto. El texto o título del enlace se pone entre `[]` y la dirección del enlace se pone a continuación entre `()`. En la dirección se puede poner el identificador de un encabezado para hacer una _referencia cruzada_. Por ejemplo, [este enlace a la página web de Google](http://www.google.es) se ha creado escribiendo:

```
[este enlace a la página web de Google](http://www.google.es)
```

>> Si hemos instalado `Markdown Editing` en Sublime entonces podemos crear rápidamente este tipo enlace escribiendo `mdl` y pulsando la tecla `Tab`.


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

---
title: Sublime y Markdown
section: 2
next: 3-markdown
prev: 1-intro
---

Los metadatos que aparecen pueden ser utilizados por pandoc para producir cierta información en los documentos generados en la conversión. Por ejemplo, los metadatos anteriores pueden ser usados (con la plantilla adecuada) para crear un HTML con el título indicado en `title`, un encabezado con el número de la sección (`section`) y unos enlaces de navegación que nos llevan al documento anterior (`prev`) y siguiente (`next`).

Los símbolos de escape llevan delante el símbolo `\`. Se pueden "escapar" los siguientes símbolos:

```
\`*_{}[]()>#+-.!
```







