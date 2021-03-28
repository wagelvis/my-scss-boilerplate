# CARPETA VENDORS

Y por último, pero no menos importante, la mayoría de los proyectos tienen una carpeta vendors/ que contiene todos los archivos CSS procedentes de librerías externas y frameworks – Normalize, Bootstrap, jQueryUI, FancyCarouselSliderjQueryPowered, etc. Poner estos archivos en una misma carpeta, es una buena forma de decir “¡Hey! esto no lo he escrito yo, no es mi código y no es mi responsabilidad”.

\_normalize.scss
\_bootstrap.scss
\_jquery-ui.scss
\_select2.scss

Si tienes que sobrescribir una sección de cualquier vendor, te recomiendo que tengas una octava carpeta llamada vendors-extensions/ en la que puedes poner estos archivos usando el mismo nombre que le ha dado el desarrollador.

Por ejemplo, vendors-extensions/\_bootstrap.scss es un archivo que contiene todas las reglas CSS que se volverán a declarar con respecto al CSS por defecto de Bootstrap. Esto se hace para evitar editar directamente los archivos del proveedor, lo que es en general una mala idea.
