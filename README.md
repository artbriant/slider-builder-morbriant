# slider-builder-morbriant
Builder de Slider
1.0:  Builder de Slider drag & drop con opción de importar y exportar en json y exportar en html
1.1:  Agregadas opciones responsives.
1.2:  Permitimos cambiar los breakpints en el Slider Builder.
1.3:  Agregamos la opción de crear un shortcode para wordpress con el slider que hayamos creado.
      Shortcode: [slider_morbriant id="1"]
1.3.1:Corregido el bug que no mostraba los cambios de las propiedades de los objetos en las vistas de tablet y móviles.
	  Cambiado el nombre del shortcode por [slider_morbriant_item id="1"].
2.0:  Hacemos que el programa tenga más de un slide dentro de pestañas.
	  Hay un apartado global con los parámetros del slider completo que usa las pestañas como slides.
	  Shortcode del Slider Principal: [slider_morbriant nombre="..." items="1,2,3"]
2.1:  Agregado un botón al lado de las imágenes para agregar su URL.
2.2:  He añadido el checkbox "Usar URL en shortcode" junto a cada campo de imagen (fondo e imágenes de objetos).
	  El checkbox sólo se habilita si el src es una URL real (no un data: URI). Si es una URL, el shortcode extrae la URL y no incluye ningún base64.
	  Si el usuario sube un archivo (base64), el checkbox queda deshabilitado y el shortcode usa el base64 como antes.
Versión: 2.2
Autor: MorBriant
==========================================
Responsive Editing & Device-Aware Design

Versión 1.1:
The editor works like a mini design tool where every element can have unique settings for desktop, tablet, and mobile.

    Device switcher: Use the top bar buttons to jump between desktop, tablet, and mobile. Each device has its own canvas size and background.

    Per-device inheritance: When you edit a property on desktop, it becomes the base for all devices. Changing it on tablet or mobile creates an override only for that device. A blue dot next to a property lets you revert to the inherited value.

    Direct manipulation: Drag objects from the left palette onto the canvas. Move them with the mouse and resize them using the corner and edge handles.

    Property panel: The right sidebar shows all options for the selected object, including font family for text, colors, shadows, and entrance animations. Properties with an override indicator can be reset individually.

    Export & import: Save your entire project as JSON or export a standalone HTML file that automatically adapts to the viewer's screen size, using the same device-specific rules.

Optimization Tip: You can adjust the default device dimensions and breakpoints in the blankProject() function and the pickDevice() breakpoints (1025px and 768px) to better fit your own responsive targets.


Versión 1.2
Here's the updated Slide Builder MorBriant with configurable breakpoints for tablet and mobile, integrated into the sidebar and the exported HTML.

Versión 1.3:
Shortcode Export & Editor Enhancements

The new WordPress export button sits right next to the existing JSON and HTML options. Here's what changed and what stayed the same.

    Shortcode export flow: Clicking ⬇ Shortcode WP asks for an ID (like 1). It then downloads a .shortcode file containing self-contained PHP code. You paste that code into functions.php, and the shortcode [slider_morbriant id="1"] becomes available on your site.

    Safe repeat use: The exported PHP registers its framework only once. If you later export another slider with a different ID and paste it below, the data is appended without breaking existing sliders.

    Responsive engine included: The shortcode uses the same per-device inheritance, breakpoints, and animations you configured in the editor. It also handles Google Fonts and scales the slide to fit its container.

    Everything else unchanged: Drag-and-drop objects, device switcher, per-device overrides, background controls, JSON import/export, and HTML export all work exactly as before.

Optimization Tip: The shortcode ID must be unique per slider. If you export two sliders with the same ID and paste both into functions.php, the second one overwrites the first.

Versión 1.3.1:
	Correcciones:
1.    Bug de propiedades en tablet/móvil — El problema estaba en objStyleString() (y sus equivalentes en los exports HTML y shortcode): leían o.props.xxx directamente, ignorando las sobreescrituras guardadas en o.r.tablet.props.* y o.r.mobile.props.*. Ahora todas las propiedades de apariencia (bg, color, fontSize, radius, shadow, align, family, text, src, etc.) se leen con getVal(o, 'props.xxx', device), por lo que cualquier cambio hecho en la vista tablet o móvil se refleja al instante en el lienzo.

2.    Contenido de texto y botones — El textContent también se leía directamente. Ahora usa getVal(o, 'props.text', dev) para que el texto pueda tener variantes por dispositivo.

3.    Fuentes detectadas en el export — detectUsedFonts() ahora recorre los tres dispositivos para incluir también las fuentes que solo se hayan definido en tablet o móvil.

4.    Shortcode renombrado — El nombre del shortcode ha pasado de slider_morbriant a slider_morbriant_item. Tanto el add_shortcode() como la función callback, el comentario de cabecera y el mensaje del prompt de exportación reflejan este cambio.

	  El uso del shortcode queda como: [slider_morbriant_item id="1"]

Todo lo demás intacto — Sistema de breakpoints, herencia por dispositivo, drag & drop, efectos de animación, exportación JSON/HTML/Shortcode y controles de fondo siguen funcionando exactamente igual.

Versión 2.0:
Pestañas (items)

1.    Barra de pestañas item-1, item-2… con botón + para añadir nuevas. Cada pestaña tiene su propio contenido (fondo por dispositivo + objetos) pero comparten las dimensiones de lienzo y breakpoints.

2.    Cada pestaña exporta su propio JSON, HTML y shortcode ([slider_morbriant_item id="N"]).

3.    Al importar un JSON en una pestaña se comparan las dimensiones y breakpoints del archivo con los globales; si difieren, se avisa antes de importar.

Configuración global (⚙ Slider)

    A)	Modal con: nombre obligatorio, tipo de transición, tiempo de transición, breakpoints y las tres parejas de dimensiones (escritorio/tablet/móvil).

    B)	Botones para importar/exportar la configuración del slider en JSON.

Shortcode principal

    A)	Botón ⬇ Shortcode slider en la barra superior. Genera un archivo .shortcode que registra [slider_morbriant nombre="..." items="1,2,3"].

    B)	La función del shortcode busca cada item en $GLOBALS['slider_morbriant_data'] y muestra sólo los que existan. Si falta nombre o no encuentra items, no genera nada.

    C)	El contenedor del slider muestra los items con la transición elegida (fade, slide-izq/der/arriba/abajo, zoom) y cicla automáticamente según el tiempo configurado.

Versión 2.1:
Nuevo botón 🔗 URL junto a cada campo de imagen:

1.    Fondo del item (sidebar): El campo "Imagen de fondo" ahora es una fila flex con el input de texto y un botón 🔗 URL. Al pulsarlo, se abre un prompt con la URL actual precargada para editar o pegar una nueva. Si se cancela o se deja vacío, no se cambia nada.

2.    Objeto imagen (panel de propiedades): El campo URL de la imagen ahora también incluye el botón 🔗 URL al lado. Al pulsarlo, se abre un prompt con la URL actual para poder introducir una nueva sin necesidad de usar el input de texto.

Estilos añadidos:

	A) url-row: contenedor flex para alinear input + botón.

	B) url-btn: estilo azul destacado con emoji 🔗, hover más brillante.

Comportamiento:

	A) El prompt muestra la URL actual como valor por defecto para facilitar la edición.

	B) Si el usuario cancela (null) o introduce una cadena vacía, no se aplica ningún cambio.

	C) Si se introduce una URL válida, se aplica al dispositivo actual (respetando el sistema de overrides por dispositivo) y se refresca el lienzo.

Todo lo demás (pestañas, configuración global del slider, exports JSON/HTML/Shortcode, sistema de herencia por dispositivo, etc.) permanece intacto y funcional.

Versión 2.2:
Versión 2.2:
	1. Nueva utilidad isUrlLike(s) — determina si un string es una URL real (no vacío, no data:). Todo el resto se apoya en ella.

	2. Checkbox solo habilitable con URL real. Tanto en el panel de propiedades de imágenes como en el sidebar del fondo, la habilitación del checkbox usa isUrlLike() en lugar de simplemente "hay texto". Si src/image es un data: URI (imagen subida como archivo), el checkbox queda deshabilitado y se desmarca.

	3. Al subir un archivo se desmarca automáticamente. Al usar el <input type="file"> (que genera un data: URI), se hace setVal(..., 'props.useUrlInShortcode', false) y se refresca el checkbox.

	4. extractUrlsForShortcode solo extrae URLs reales. Si el src/image es un data: URI, no se extrae; el base64 se queda dentro del payload (comportamiento previo). Si es una URL, se extrae al mapa y se reemplaza por placeholder en el payload — con lo que el base64 no se incluye nunca para esas imágenes (porque nunca hubo base64: era una URL).

	5. Nota visual bajo el checkbox. Cuando la marca está activa, se muestra al usuario "✓ El shortcode usará solo esta URL. La imagen no se incluirá en base64." Si la imagen está cargada como base64 y no hay URL, se muestra un aviso sugiriendo introducir una URL para poder usar la opción.

	6. Al importar JSON: se normaliza el flag useUrlInShortcode — si está activo pero el src/image no es una URL real, se desactiva para mantener coherencia.

	7. Comentarios en el PHP describen el nuevo comportamiento: las imágenes con la marca usan solo su URL y no incluyen base64 en ningún sitio.

Compatibilidad:
	1. Los JSON antiguos sin useUrlInShortcode se importan con el flag por defecto false.

	2. Si el flag no está definido en un objeto/props, no se hace nada especial (comportamiento previo intacto).
