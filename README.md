# slider-builder-morbriant
Builder de Slider
1.0:  Builder de Slider drag & drop con opción de importar y exportar en json y exportar en html
1.1:  Agregadas opciones responsives.
1.2:  Permitimos cambiar los breakpints en el Slider Builder.
1.3:  Agregamos la opción de crear un shortcode para wordpress con el slider que hayamos creado.
      Shortcode: [slider_morbriant id="1"]
1.3.1:Corregido el bug que no mostraba los cambios de las propiedades de los objetos en las vistas de tablet y móviles.
	  Cambiado el nombre del shortcode por [slider_morbriant_item id="1"].
Versión: 1.3.1
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
