# Frontend Mentor - 3-column preview card component solution

------



## Table of contents

- Descripción general
  - El desafío
  - Links
- Mi proceso
  - Construido con
  - Que aprendí
  - Desarrollo continuo
  - Recursos útiles
- Autor

------

## Descripción general

### El desafío

Los usuarios deben poder:

- Ver el diseño óptimos según el tamaño de pantalla
- Ver estados de desplazamientos para elementos interactivos

### Links

- Solution URL: [Add solution URL here](https://your-solution-url.com)
- Live Site URL: [Add live site URL here](https://your-live-site-url.com)

## Mi proceso

### Contruido con

- Marcado semántico HTML5
- CSS flexbox
- Responsive design
- Media Queries
- Desktop first
- Medidas relativas al contenedor (%) y relativas al viewport (vh)
- Medidas relativas a la fuente en pixeles (rem y em)
- Metodología BEM

### Que aprendí

 El desafío presentaba un diseño de tres columnas dónde debía de presentarse en tamaño de escritorio y adaptarse a la vista de mobil. En un principio decidí trabajarlo con CSS grid, pero, al ahondar en la teoría de los mismos he entendido que el CSS grid está pensado para construcciones bidimensionales, es decir, filas  y columnas. SIn embargo, para en este caso, necesitaba un diseño unidemensional cómo CSS flexbox, es decir, filas o columnas. En efecto, he decido trabajar con este último y aprovechar los anchos mínimos y el flex wrap para convertir de filas a columnas cuándo la ventana del navegador comience a hacerse más pequeña y obtener, en efecto, el diseño responsive.

```css
.cards {
    display: flex;
    flex-flow: row wrap;
}
```

Establecí un alto mínimo de 100vh para el body con su respectivo posición relativa para dejar al footer siempre abajo con una posición absoluta y un bottom 0. Luego construí un alto fijo para el contenedor de 60vh con sus respectivo márgenes para que todo el proyecto se encuentre en ese 100% del alto del viewport. El problema fue que cuándo llevaba el tamaño de la ventana a vista mobil, el contenido desbordaba y el footer se rompía. Luego de pensar el problema me he dado cuenta que necesitaba hacer dos cosas: la primera era no establecer un alto fijo en el contenedor, sino un alto mínimo, para que de esta manera alcance el mínimo de 60vh y provocar que el alto sea automático y siga creciendo según crezca en contenido. Lo segundo fue colocar un padding bottom al body para que siempre se respete la distancia entre el footer y la parte de abajo del contenedor y mantener la proporcionalidad sin que se rompa el diseño.

```css
.cards {
    min-height: 60vh;
}

  
```
```css
body {
    padding-top: 20vh;
    padding-bottom: 20vh;
}
```

El tercer problema fue trabajar con los componentes internos de la tarjeta.  Se intentó trabajar sin flexbox en un principio y con medidas absolutas (píxeles), lo cuál no fue una idea conveniente para lograr el diseño responsivo. Asi que he decido trabajar con flexbox y un flex direction column. Para lograr que el botón esté siempre debajo y el ícono siempre arriba, opté por un justify content space between

```css
.card {
    display: flex;
    flex-flow: column wrap;
    justify-content: space-between;
    align-items: flex-start;
}

```

El problema era que el título y el párrafo quedaban centrado y no quería moverlos con position relative debido al llevar el diseño a mobile, al trabajar con ems y al hacerse más pequeño el tamaño, podía generar una desproporción. Por este motivo se colocó el ícono y el párrafo un un div y de esa manera se pegaban a la parte superior mientras el botón en la parte inferior y, a partir de allí trabajar con márgenes hasta quedar en posiciones aceptables.

```html
<div class="cards">
      <section class="card card--orange">
        <div class="card__content">
          <img src="#" alt="sedans icon" 	class="card__icon">
          <h2 class="card__title">Sedans</h2>
          <p class="card__paragraph">
            Choose a sedan for its affordability and excellent fuel economy. Ideal for 				cruising in the city 
            or on your next road trip.
          </p>
        </div>
        <a href="#" class="card__button card__button--orange">Learn More</a>
      </section>
```

```css
.card {
    display: flex;
    flex-flow: column wrap;
    justify-content: space-between;
    align-items: flex-start;
    flex-grow: 1;
    width: 33.33%;
    min-width: 300px;
    height: auto;
    padding: 2.8em 4em 2.8em 2.8em;
}
```

Aquí vemos, precisamente en la última linea, que hemos establecidos determinados paddings para que el space between no quede debajo rozando los bordes inferiores y superiores, y padding laterales para lograr el diseño lo más parecido posible

```css
.card__icon {
    margin-bottom: 2.8em;
}

.card__title {
    margin: 0;
}

.card__paragraph {
    margin-top: 2.8em;
}
```

Por último, pero no menos importante, se enfrentaba el problema de las proporciones al cambiar desde vista de escritorio hacia vista mobil. Luego de investigar, se decidió trabajar con Media Queries cón unos determinados píxeles en tamaño de fuente para la vista mobil y otros determinados píxeles para la vista de escritorio y, al trabajar con ems todo lo demás, el diseño se adaptaba excelentemente de una vista a la otra debido que los ems son relativos al tamaño de fuente y, este último cambiaba de acuerdo a las diferentes vistas y, en efecto, se modificaba proporcionalmente las proporciones y lograr el diseño resposivo.

```css
@media screen and (min-width: 375px) {
    body {
        font-size: 15px;
    }
}

@media screen and (min-width: 1440px) {
    body {
        font-size: 17px;
    }
```

```css

.cards {
    min-height: 60vh;
    width: 55%;
    min-width: 300px;
    border-radius: 8px;
}

.card {
    width: 33.33%;
    min-width: 300px;
    height: auto;
    padding: 2.8em 4em 2.8em 2.8em;
}


.card__icon {
    margin-bottom: 2.8em;
}

.card__title {
    margin: 0;
    font-family: 'Big Shoulders Display', cursive;
    font-size: 2.8rem;
    font-weight: 700;
}

.card__paragraph {
    margin-top: 2.8em;
    line-height: 1.7em;
}

.card__button {
    width: 10em;
    height: 3.3em;
    border-radius: 30px;

}

.attribution {
    font-family: 'Big Shoulders Display', cursive;
    font-size: .8rem;
    font-weight: 700;
    letter-spacing: .1em;
}

```

<!--Nota: Se han mostrado las declaraciones y propiedadaes relevantes de acuerdo a las explicaciones. Por lo tanto, las que no servían de ejemplo directo se han ocultado. Para más información ver el código completo en el repositorio.-->

### Desarrollo continuo

Me gustaría seguir perfeccionandome en las Media Queries y css flexbox. Además tengo la intención de internalizar de manera práctica css grid en proyectos posteriores y comenzar a trabajar con animaciones y transiciones. 

Por otro lado sigo utilizando la metodología BEM, pero me gustaría conocer otras metodologías de arquitectura CSS además de la presente.

He investigado y hay consejos sobre utilizar ems en los breakpoints para las Media Queries, he leído algunos artículos pero aún no logro entender el motivo. 

### Recursos útiles

- [https://www.youtube.com/watch?v=udGrXWeJp1Y&t=8990s](https://www.example.com) - Curso de arquitectura  CSS y responsive design. He entendido sobre las medidas relativas utilizadas para el diseño responsive, el uso de Media Queries y los breakpoints.
- https://xitrus.es/blog/91/Adapta_el_texto_en_Responsive_Designs - En este artículo pude comprender la relación entre píxeles, rems y ems junto a las Media Queries.
- [https://cloudfour.com/thinks/the-ems-have-it-proportional-media-queries-ftw/ - En este artículo he realizado la busqueda por entender por que utilizar ems en los breakpoints, aunque sigo sin entenderlo.
- https://www.youtube.com/watch?v=eB02fMwnOCE&t=523s - Esta es una solución que encontré en YouTube dónde se consideró utilizar flexbox y jugar con el justify content y el aligns item en los componentes internos de la tarjeta.
- https://www.youtube.com/watch?v=2Wy_MJPDfCw&t=1112s Esta solución me ayudó a enteneder la importancia del uso de los paddings y cómo podía relacionarlo con flexbox utilizando un justify content space between con un flex direction column y, de esa manera, dejar el botón simpre debajo pegado a la parte superior del padding bottom.

## Autor

- Website - [Ezequiel Vélez] (https://github.com/velzeq7)
- Frontend Mentor - [@velzeq7] (https://www.frontendmentor.io/profile/velzeq7)
