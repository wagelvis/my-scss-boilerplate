# Documentación SASS

https://sass-lang.com/documentation

# COMPILACIÓN SCSS TO CSS

## UNMINIFY

sass --watch main.scss ../css/styles.css

## MINIFY

sass --watch --style=compressed main.scss ../css/styles.min.css

# ARQUITECTURA SASS

Referencia: https://sass-guidelin.es/es

## Archivo main.scss

El archivo principal (normalmente llamado main.scss) debería ser el único archivo Sass de todo el código que no empieza con guión bajo. Este archivo no debería contener nada más que @import y comentarios.

Los archivos deben de importarse según la carpeta que los contiene, una después de la otra en el siguiente orden:

abstracts/
vendors/
base/
layout/
components/
pages/
themes/

Con el fin de mantener la legibilidad, el archivo principal debe respetar las siguientes pautas:

un archivo para cada @import;
un @import por línea;
no dejar una línea en blanco entre dos archivos que pertenecen a la misma carpeta;
dejar una línea en blanco después del último archivo de una carpeta;
las extensiones de archivo y los guiones principales se omiten.

@import 'abstracts/variables';
@import 'abstracts/functions';
@import 'abstracts/mixins';
@import 'abstracts/placeholders';

@import 'vendors/bootstrap';
@import 'vendors/jquery-ui';

@import 'base/reset';
@import 'base/typography';

@import 'layout/navigation';
@import 'layout/grid';
@import 'layout/header';
@import 'layout/footer';
@import 'layout/sidebar';
@import 'layout/forms';

@import 'components/buttons';
@import 'components/carousel';
@import 'components/cover';
@import 'components/dropdown';

@import 'pages/home';
@import 'pages/contact';

@import 'themes/theme';
@import 'themes/admin';

Hay otra forma de importar las partes de un proyecto que también que me parece válida. La parte positiva, es que hace que el fichero sea más legible. Pero por otro lado, actualizar el contenido puede ser un poco más doloroso. De todas formas, te dejaré decidir qué es lo mejor, en realidad no importa demasiado. Para hacer las cosas de esta manera, el archivo principal debe respetar las siguientes pautas:

un @import por carpeta;
un salto de línea después de cada @import;
cada archivo debe ir en su propia línea;
dejar una línea en blanco después del último archivo de una carpeta;
las extensiones de archivo y los guiones principales se omiten.

@import
'abstracts/variables',
'abstracts/functions',
'abstracts/mixins',
'abstracts/placeholders';

@import
'vendors/bootstrap',
'vendors/jquery-ui';

@import
'base/reset',
'base/typography';

@import
'layout/navigation',
'layout/grid',
'layout/header',
'layout/footer',
'layout/sidebar',
'layout/forms';

@import
'components/buttons',
'components/carousel',
'components/cover',
'components/dropdown';

@import
'pages/home',
'pages/contact';

@import
'themes/theme',
'themes/admin';

## El Archivo de la Verguenza

Hay un concepto interesante que ha popularizado Harry Roberts, Dave Rupert y Chris Coyier y que consiste en poner todas las declaraciones CSS, hacks y cosas de las que no nos sentimos muy orgullosos en un archivo de la verguenza. Este archivo, titulado dramáticamente \_shame.scss, se importará después de los demás archivos, al final de la hoja de estilo.

/\*\*

- Arreglo específico para la navegación
-
- Alguien utilizó un ID en el código del _header_ (`#header a {}`) lo que sobreescribe a
- los selectores nav (`.site-nav a {}`). Usar !important para anularlo hasta que
- tenga tiempo de arreglarlo.
  \*/

.site-nav a {
color: #BADA55 !important;
}

# Breakpoints - Puntos de ruptura

Creo que puedo decir con seguridad que las media queries no deberían estar vinculadas a dispositivos específicos. Por ejemplo, es una mala idea intentar trabajar con tamaños específicos para iPads o Blackberry. Las media queries deberían trabajar con un rango de tamaños de pantalla, justo hasta que el diseño se rompa y la siguiente media query haga su función.

Por las mismas razones, los puntos de ruptura no deberían llevar el nombre de los dispositivos, sino algo más general. Sobre todo porque algunos teléfonos son ahora más grandes que algunas tablets, algunas tablets más grandes que un ordenador pequeño y así sucesivamente…

// Yep
$breakpoints: (
'medium': (min-width: 800px),
'large': (min-width: 1000px),
'huge': (min-width: 1200px),
);

// Nope
$breakpoints: (
'tablet': (min-width: 800px),
'computer': (min-width: 1000px),
'tv': (min-width: 1200px),
);
Llegados a este punto, cualquier nomenclatura que deje claro que el diseño no está ligado a un dispositivo en concreto podría funcionar, siempre y cuando tenga un sentido de magnitud.

$breakpoints: (
'seed': (min-width: 800px),
'sprout': (min-width: 1000px),
'plant': (min-width: 1200px),
);

Los ejemplos anteriores utilizan mapas anidados para definir los puntos de ruptura, sin embargo, esto depende de qué tipo de gestor de breakpoints utilices. Puedes optar por cadenas en lugar de mapas para una mayor flexibilidad (por ejemplo '(min-width: 800px)').

## Gestor De Puntos De Ruptura

Una vez que tus breakpoints tengan la nomenclatura deseada, necesitas una manera de utilizarlos en las media queries reales. Hay un montón de maneras para hacerlo, pero tengo que decir que soy un gran fan del mapa de puntos de ruptura (breakpoint map) leído por una función getter. Este sistema es tan simple como eficiente.

/// Gestor Responsive
/// @access public
/// @param {String} $breakpoint - Punto de ruptura
/// @requires $breakpoints

@mixin respond-to($breakpoint) {
  $raw-query: map-get($breakpoints, $breakpoint);

@if $raw-query {
    $query: if(
      type-of($raw-query) == 'string',
unquote($raw-query),
      inspect($raw-query)
);

    @media #{$query} {
      @content;
    }

} @else {
@error 'No se ha encontrado un valor para `#{$breakpoint}`. ' + 'Por favor, asegúrate que está definido en el mapa `$breakpoints`.';
}
}

Obviamente, este es un gestor de puntos de ruptura bastante simplista. Si necesitas un gestor ligeramente más permisivo, te recomiendo que no reinventes la rueda y utilices algo que ya esté probado y comprobado, como por ejemplo Sass-MQ, Breakpoint o include-media.

Si estás buscando más información acerca de cómo enfocar las Media Queries en Sass, tanto SitePoint (de este servidor) como CSS-Tricks tienen muy buenos artículos al respecto.
