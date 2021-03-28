# CARPETA BASE

La carpeta base/ contiene lo que podríamos llamar la plantilla del proyecto. Allí, puedes encontrar el archivo reset para reiniciar los estilos CSS, algunas reglas tipográficas y probablemente un archivo CSS que define algunos estilos estándares para los elementos HTML más comunes (y que me gusta llamar \_base.scss).

\_base.scss
\_reset.scss
\_typography.scss

Si tu proyecto usa muchas animaciones CSS, podrías pensar en añadir un archivo \_animations.scss conteniendo las deficiones de @keyframes de todas tus animaciones. Si solo las usas esporádicamente, déjalas convivir con los selectores que las usan.
