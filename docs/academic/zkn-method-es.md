# El Método del Zettelkasten (fichero)

Tuve la idea para desarrollar Zettlr hace unos años cuando intentamos elaborar buenos flujos de trabajo para textos académicos. Probamos muchos estilos y flujos de trabajo diferentes y uno que enganchó fue el método del Zettelkasten. El problema entonces era que la mayoría del software no implementó el método con éxito. Desde entonces ha habido puesto mucho esfuerzo en integrar el método así que hoy en día hay más y más aplicaciones que implementan algunas funcionas de este método. 

Originalmente, el método se basa en el sociólogo alemán Niklas Luhmann, quién diseño su propio fichero (en aquel entonces análogo) conteniendo fichas con información y algunos números. Los números podían ser usados para localizar otras fichas con otra información en alguna manera relacionada con el contenido de la primera ficha. De esta manera Luhmann podía hacer referencia por atrás y por delante entre conjuntos de fichas hasta que la caja del fichero se llenó y llegó a una masa crítica que le permitió al fichero desarrollar una "vida propia", mostrando a Luhmann conexiónes entre ciertos conceptos que él, Luhmann, no había pensado.

La idea basica es, por tanto, dejarte crear erlaciones entre fichas, pequeñas notas (o bien, para aquel asunto, archivos LARGOS) no solo para permitirte mover por delante o por atrás entre archivos, pero también permitirte identificar relaciones que emergen entre tus archivos.

## Administrar un Zettelkasten (fichero) con Zettlr

Actualmente hay tres funciones disponible para arrancar tu propio Zettelkasten (fichero):

1. Generación de identificaciones (ID) de archivos Vinculación de búsqueda y archivos  Utilización de tags (etiquetas)

### Identificación de archivos

Uno de los problemas más grandes en desarrollar apps que intentan no añadir a los archivos contenido que es especifico de la app es la identificación del archivo.  Internamente, Zettlr utiliza un hash de 32 bit cada archivo para identificarlo. Dependen en las paths (rutas) y entonces no sirven en el entorno cloud (nube), aunque Zettlr está diseñado para usarlo, ya que las rutas en un ordenador serán diferentes de las de otro. La segunda dificultad es por el formato mismo: archivos de tipo markdown son de texto sencillo y por tanto no permiten añadir tantos metadatos. Naturalmente, habían intentos de integrar cabeceras en archivos markdown, pero eso realmente no fue la manera adecuada de seguir, ya que hacerlo pondría en peligro la regla de Zettlr de escribir archivos agnósticos de tipo  markdown. Metadatos son mucho menos estandardizados que la sintaxis del Markdown mismo, haciéndolo complicado imaginarse como eso podría cooperar con la filosofía de Zettlr.  La solución que hemos encontrado es simplemente poner IDs en algún lado del texto. Para insertar una ID en el texto, simplemente pulsa `Cmd/Ctrl+L` para generar una o escribela tú. La ID se destacará automagicamente.

> Echa un vistazo a la [pagina de ajuntes](../reference/settings-es.md) para ver las opciones de como personalizar toda la funcionalidad del Zettelkasten (fichero) a tu gusto.

La ID por defecto es una buena decisión, porque utiliza la fecha en el formato AAAAMMDDHHMMSS, el cuál es único hasta el segundo. También según nuestras experiencias propias, en usar IDs fácilmente a reconocer uno es menos propenso de asumir cosas, haciéndoles más adecuado para referencias cruzadas. ¡Inténtalo!

Zettlr intentará encontrar automáticamente la ID de un archivo a través de buscar su contenido. Si se encuentra una ID que _no_ es encapsulada por un enlace estilo Wiki (más sobre el tema abajo), va a asumir esta ID internamente para referirse a un archivo. Si hay más que una ID en el archivo, **la primera ID tomará prevalencia**. De este modo, incluso en archivos largos, si no puedes encontrar la ID, simplemente pega nueva ID arriba del archivo para tomar la función de la ID general de este archivo. 

### Vinculación interna

Una vez el problema de la identificación estuvo solucionado, otro problema ocurrió: ¿Cómo vincular archivos a través de la app sin poner en peligro los objetivos de Zettlr mencionado arriba de crear archivos que son independientes de la app? Muchas apps como nvALT o The Arvchive implementan un sistema interna de vinculación que lo hace posible hacer referencia a archivos de uno al otro para facilitar la navegación a través del sistema. Zettlr también incluye tal sistema.

Un enlace interno se escribe con la sintaxis de `[[Este es el enlace]]`. Si haces clic en ello mientras pulsas `Alt` o `Ctrl`, se disparan **dos** funciones distintas: Primero, se intenta encontrar en el contenido de la app una correspondencia precisa del enlace. Esto significa que se intenta encontrar un archivo que indica de que su contenido coincide perfectamente con el enlace. eUna coincidencia tan exacta se puede encontrar de dos maneras: Primero, si el contenido del enlace (en el ejemplo anterior "Este es el enlace") **exactamente** coincide con un nombre de archivo, excluyendo su extensión, el archivo correspondiente informará de que se trata de una coincidencia exacta. El ejemplo anterior coincidiría exactamente con los archivos `Este es el enlace.md`, `Este es el enlace.markdown` y `Este es el enlace.txt`. Ten en cuenta que la comparación de nombres de archivo se realiza **sin distinguir entre mayúsculas y minúsculas**. macOS, por ejemplo, no distingue mayúsculas de minúsculas (por lo que `filename.md` coincidiría con el mismo archivo que `FILENAME.MD`). La segunda forma en que un enlace de este tipo puede dar lugar a una coincidencia exacta sería si el contenido del enlace contiene una ID en el formato `[[<tu-id>]]`. Si algún archivo tiene la ID `<tu-id>`, Zettlr también producirá una coincidencia exacta. **Si se encuentra una coincidencia exacta en algún lugar del sistema, un Alt-Clic en un enlace interno abrirá inmediatamente el primer archivo coincidente**. Esto quiere decir que puedes utilizar dichos enlaces para navegar por tu sistema. Puedes, por ejemplo, acomodar esta funcionalidad creando archivos de índice que contengan enlaces internos a varios archivos, y en cada uno de estos archivos, colocas un enlace que regrese al archivo de índice respectivo.

La segunda función que se dispara por tal enlace es una búsqueda global dentro del directorio actualmente seleccionado. Simplemente tomará el contenido del enlace, lo colocará en el cuadro de búsqueda y automáticamente pulsará "Enter" para iniciar la búsqueda. De esta manera, no sólo podrás abrir archivos exactos, sino que también podrás encontrar todos los demás archivos que enlazan con el archivo que acabas de abrir. Así que un enlace en el formato `[[<tu-id>]]` abriría ese archivo específico y también buscaría todos los archivos que enlazan con ese archivo.

### Utilizar tags (etiquetas)

El etiquetado puede ser la forma más fácil de búsqueda interna. Si haces `Alt`- o `Ctrl`-Clic en una etiqueta, esto simplemente hará una búsqueda de todos los archivos en tu carpeta actual que están marcados con esta etiqueta.
 Como las etiquetas en la forma `#PalabraClave` no se utilizan en ninguna parte de la sintaxis Markdown, el uso de este enfoque permite a Zettlr utilizar dichas etiquetas como el medio perfecto para crear un sistema de etiquetado.