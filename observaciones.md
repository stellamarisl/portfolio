# Observaciones

Querida Estela, felicitaciones! Que hermoso trabajo entregaste. Me encantan los colores, la tipografia, todo tu portfolio se ve muy lindo y se nota muchísimo el esfuerzo por hacer que se asemeje al modelo de Ada.

El mayor problema en tu portfolio es que el responsive no funciona, lo que afecta negativamente tu nota a pesar de que se nota que pusiste esfuerzo. Seria una nota muchisimo mas alta si eso estuviera, pero una web sin responsive no está completa: la mayoría de nuestros usuarios van a ver nuestra web desde el celular, por lo que es absolutamente necesario poder ofrecerles la misma experiencia a ellos. Noto muy poquitas media queries, por lo que no sé si te faltó tiempo o no lo pudiste resolver. Si es el segundo caso, me escribirías? Asi podemos verlo juntas más en detalle.

Te dejo varios comentarios para mencionar cositas puntuales. Como comentamos en clase, este trabajo no se hace para que constates conocimientos, sino para que aprendas: en ese sentido, mi intencion es que estos comentarios te sirvan para aprender, mejorar tu codigo a futuro e ir apreciando mejor qué se espera de nosotras como desarrolladoras front end. 

## Estructura correcta de documento HTML

Tu HTML esta muy bien. Claro, prolijo, sin elementos de más, muy bien comentado.

Algo que me llama la atención es tu `head`, dado que allí repetís innecesariamente el link de google fonts. No es necesario escribilo dos veces

```html
    <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@500&display=swap" rel="stylesheet">
    <link rel="preconnect" href="https://fonts.gstatic.com">
    <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@600&display=swap" rel="stylesheet">
    <link rel="preconnect" href="https://fonts.gstatic.com">
    <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@900&display=swap" rel="stylesheet">
```

Cada uno de esos links hace exactamente lo mismo - traerse el css de google fonts para poder usar los fonts en tu sitio, con la diferencia de los weight en 500, 600 y 900. Quizá estés bajo la impresión de que por cada uno de los fonts de tu web es necesario traerse nuevamente el css, pero no, no es necesario agregarlo más de una vez. Agregar muchos de estos links innecesarios impacta negativamente en la velocidad de carga de tu web, ya que por cada uno de ellos se hace un llamado a un css externo y se lo carga. Podemos hacerlo todo de una asi:

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@500;600;900&display=swap" rel="stylesheet">
```

Tres cosas que haces ocasionalmete en tu HTML:
- usar etiquetas `br` para separar las cosas
- usar la etiqueta `<strong>` para darle grosor al texto
- usar "width" y "height" en el html. 
No llegué a comentarlo en clase, pero esto es incorrecto. Esas etiquetas son un resabio de viejas épocas en las cuales css no era tan poderoso como ahora, pero usarlas hoy viola uno de los principios básicos de programación: la separación de responsabilidades. Los estilos se dan con css, la estructura se da con html. Una decisión de estilo como un espaciado entre dos elementos debe controlarse con css -flex, elementos en bloque, etc, no con `br`.

## Respeta la consigna

- El portfolio cuenta con las secciones solicitadas

Cumplido

- Al clickear en los links de navegación, debe llevar a la sección correspondiente

Cumplido. Un comentario en tu botón "lo que hago": fijate que para que funcione el link debes hacer click especificamente en el texto. Si haces click en el boton, pero no en el texto (a los costados del boton por ejemplo) el link no anda. 

La etiqueta `a`, debe rodear a un elemento para que el link funcione en ese elemento. En tu caso, el link esta adentro del boton, rodeando al texto: solo el texto es un link, no el boton en si. La etiqueta `a`deberia estar por fuera del boton, asi:

```html
<a href="#proyectos">
    <div class="btn btn-loque">
        Lo que hago
    </div>
</a>
```
- Al clickear en los links de contacto, debe llevar a la página externa
  correspondiente

Cumplido.

- El portfolio debe tener un diseño responsivo y verse correctamente en distintos dispositivos

No cumplido. Comenté en clase que la guia de bootstrap para las media queries me parece la mejor, te la dejo acá. Esto nos permite enfocarnos en los tamaños mas habituales, y a la vez asegurarnos de que no dejamos afuera a ningún dispositivo.

```css
/* Celulares */
@media (max-width: 576px) {
  ...;
}

/* Celulares en modo horizontal y tablets pequeñas */
@media (max-width: 768px) {
  ...;
}

/* Tablets  */
@media (max-width: 992px) {
  ...;
}

/* Monitores pequeños */
@media (max-width: 1200px) {
  ...;
}

/* Monitores grandes */
@media (max-width: 1400px) {
  ...;
}
```

Noto que tenes media queries para 600px, pero no alcanzan ni permiten que tu web se pueda navegar en celulares. Por favor escribime si algo te genera dudas sobre el responsive, por ahora te comento un par de cositas. 

Repetis varias veces "@media (max-width: 600px){" para cada uno de tus elementos. No es necesario, podes poner todos ellos bajo la misma media query, por ejemplo asi:

```css
@media (max-width: 600px){
    .contenedor-cita{
        background-color: #ffd78e;
        width: auto;
    }
    .contenedor-formulario{
        width: auto;
        background-color: #ffd78e;
        flex-direction: column;
    }
} 
```

En general arrancas de una buena base para el responsive, darle flex-direction column a tus contenedores, pero la confusion esta en a qué elemento le das esta propiedad. Como ves, en tu codigo darle flex-direction: column a "contenedor-formulario" no hace nada. Eso es porque contenedor-formulario es un div que tiene solo un descendiente, por lo que flex no tiene impacto ahi. Compará con darle esa misma orden a "contenedorcontacto-escribo": ahora tu formulario es mucho mas responsive en celulares. 

- El portfolio debe estar deployado y ser accesible desde una URL

Cumplido, pero esta URL debe estar en el readme.

- El repositorio en GitHub debe tener un readme adecuado

Cumplido salvo por la URL. Me gustó muchisimo tu readme. 

### Respeta el diseño dado

Cumplido. Hay algunas cositas a mejorar:

- La barra de navegación superior se ve como "transparente" cuando hacemos scroll. Para solucionarlo, dale "z-index: 1" a "contenedor-nav". 

- Los elementos del formulario tienen el problema de que los textos (el placeholder o lo que el usuario escribe) se ven algo pegoteados a los bordes. Se arregla dandoles un poquito de padding (por ejemplo, 3px de padding a cada input)

- La tipografia de "descripcion" no esta definida, y por lo tanto se ve como Times New Roman, a diferencia del resto de tu web que esta con Montserrat. Noto que repetis muchas veces a lo largo de tu codigo CSS la orden "font-family: 'Montserrat', sans-serif;": eso no es necesario. La propiedad de tipografia se hereda, por lo que alcanza darla una sola vez en el body para que se aplique a todos tus elementos. 

### Buena estructura de proyecto

Cumplido.

### Código bien indentado

En general, cumplido. Ocasionalmente lo dejas pasar, como aca:

```html
     <div class="caja-logo-html">
                         <div class="html">
                         <img src="img-conocim/html-5.png" width="75px" height="76px"/>
                         </div>
                         <div class="texto-html5">
                         <p><strong>HTML 5</strong></p>
                         </div>
                 </div>
```

Recordá que siempre podés hacerlo automaticamente con VSCode haciendo click derecho + format document, pero yo te recomiendo que te acostumbres a tabular bien sola. Es muy importante para entender qué cosa está adentro de otra. Cada vez que abris una etiqueta, el contenido de esa etiqueta debe ir un espaciado hacia adentro. Asi:

```html
<div class="caja-logo-html">
    <div class="html">
        <img src="img-conocim/html-5.png" width="75px" height="76px"/>
    </div>
    <div class="texto-html5">
        <p><strong>HTML 5</strong></p>
    </div>
</div>
```


En tu CSS el tabulado está perfecto salvo en .boton-enviar. Otra cosa a mencionar es que a veces no dejas el espaciado correcto en cada orden. En lugar de escribir por ejemplo `.name{`, deja un espacio entre el nombre de la clase y la llave: `.name {`

### Comentarios que permiten mejorar la legibilidad del código

Cumplido. 

### Uso correcto de etiquetas semánticas

Cumplido. 

### Buenos nombres de clases

Cumplido.

### Código CSS bien estructurado

Cumplido. Noto algunos estilos innecesarios o confusos: ya te comenté que es innecesario repetir la tipografia. Usas varias veces "flex-direction: row;", que no es necesario ya que ese es el estilo por defecto. Lo mismo con "width: auto" (a menos que estes en una media query y estes reemplazando el width anterior). 

Usas muchas veces "position: relative" para acomodar sutilmente las cosas unos px a la derecha o hacia abajo. Te diria que en esos casos, si lo podes solucionar con un `margin` o `padding`, va a ser mejor a la larga. 

### Reutilización de estilos

Tus tarjetas de conocimientos son todas iguales, y sin emargo tienen todas clases distintas. Por ejemplo para HTML: "caja-logo-html", "html", "texto-html5" y para CSS: "caja-logo-css", "css" y  "texto-css". Sin embargo tienen los mismos estilos...! La idea de las clases es justamente que todos los elementos que son iguales tengan el mismo nombre de clase. Podrías haberle dado a cada uno de esos elementos el mismo nombre, "caja-logo-conocimiento", "conocimiento" y "texto-conocimiento"  por ejemplo, y sólo tendrías una clase para cada uno de ellos. No repetirnos a nosotras mismas es un principio muy importante en programación, porque en la repetición se encuentran buena parte de nuestros errores. Reutilizá tus clases siempre que puedas. 

### Cumple con criterios básicos de accesibilidad

- Los colores tienen un contraste adecuado

Cumplido

- Las imágenes tiene el atributo `alt` que corresponde

Cumplido, aunque es innecesario que incluyas "imagen" en la descripción ya que el lector lo informa antes de leer tu alt. 

- Los íconos y elementos que no presentan texto agregan la información correspondiente por otros medios (etiquetas aria, texto oculto)

No tenes iconos por lo que veo, usas imagenes que siempre tienen alt, asi que doy esto por cumplido. 

- Los íconos y elementos que no necesitan ser anunciados por un lector de pantalla tienen la etiqueta aria correspondiente

No veo ejemplos en tu portfolio, pero tampoco veo que sea necesario.

- Commits con mensajes adecuados

No cumplido, tenes poquitos commits. Mientras mas, mejor para mi, y mejor para tus compañeros de equipo cuando trabajes en grupo. 

- Cuenta con un favicon

No cumplido. 

### Nota: 7
