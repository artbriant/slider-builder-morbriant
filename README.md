# slider-builder-morbriant
Builder de Slider
1.0:  Builder de Slider drag & drop con opción de importar y exportar en json y exportar en html
1.1:  Agregadas opciones responsives.
Versión: 1.1
Autor: MorBriant
==========================================
Responsive Editing & Device-Aware Design

The editor works like a mini design tool where every element can have unique settings for desktop, tablet, and mobile.

    Device switcher: Use the top bar buttons to jump between desktop, tablet, and mobile. Each device has its own canvas size and background.

    Per-device inheritance: When you edit a property on desktop, it becomes the base for all devices. Changing it on tablet or mobile creates an override only for that device. A blue dot next to a property lets you revert to the inherited value.

    Direct manipulation: Drag objects from the left palette onto the canvas. Move them with the mouse and resize them using the corner and edge handles.

    Property panel: The right sidebar shows all options for the selected object, including font family for text, colors, shadows, and entrance animations. Properties with an override indicator can be reset individually.

    Export & import: Save your entire project as JSON or export a standalone HTML file that automatically adapts to the viewer's screen size, using the same device-specific rules.

Optimization Tip: You can adjust the default device dimensions and breakpoints in the blankProject() function and the pickDevice() breakpoints (1025px and 768px) to better fit your own responsive targets.
