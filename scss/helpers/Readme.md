# CARPETA HELPERS

La carpeta helpers/ reúne todas las herramientas y helpers de Sass utilizados en todo el proyecto. Cada variable global, función, mixin y placeholder debería estar en esta carpeta.

La regla de oro para esta carpeta es que no debe generar ni una sola línea de CSS cuando se compila por si sola. Solo hay helpers de Sass.

\_variables.scss
\_mixins.scss
\_functions.scss
\_placeholders.scss

Cuando se trabaja en un proyecto muy grande, con muchas utilidades abstractas, podría ser interesante agruparlas por tema en vez de por tipo, por ejemplo tipografía (\_typography.scss), temas ( \_theming.scss), etc. Cada archivo contiene todos los helpers relacionados: variables, funciones, mixins y placeholders. Hacerlo provoca que que el código sea más fácil de navegar y mantener, especialmente cuando los archivos son muy largos.

La carpeta helpers/ también se puede llamar utilities/ o abstracts/, dependiendo de tus preferencias.
