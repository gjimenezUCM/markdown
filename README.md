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





