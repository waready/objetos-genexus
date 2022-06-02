# Query


<!-- ## Browser API Access Restrictions

Because VuePress applications are server-rendered in Node.js when generating static builds, any Vue usage must conform to the [universal code requirements](https://ssr.vuejs.org/en/universal.html). In short, make sure to only access Browser / DOM APIs in `beforeMount` or `mounted` hooks.

If you are using or demoing components that are not SSR friendly (for example containing custom directives), you can wrap them inside the built-in `<ClientOnly>` component:

## -->

Se presenta el objeto Query, su estructura y conceptos fundamentales. Se explican paso a paso la construcción de un par de consultas que se visualizan en ejecución mediante gráficos en web panels.

## Funcionalidad Gx

Los Objetos [Query](https://training.genexus.com/es/aprendiendo/pdf/disenando-consultas-dinamicas-objeto-query-pdf-6098967) son consultas las cuales pueden generar diferentes tipos de graficos algo como los conocidos [chartjs](https://www.chartjs.org/) la diferencias es que al ser una consulta se puede establecer los datos especificos que se quiere visulidar especialmente para `Reportes` o `Fluctuaciones` de Datos.
Podemos necesitar agrupar la información por uno o varios criterios, realizar cálculos, y
visualizar finalmente el resultado en una forma particular

---------------------------------------------------------------------
<img :src="$withBase('/img/10.png')">

---------------------------------------------------------------------
<img :src="$withBase('/img/11.png')">

---------------------------------------------------------------------
<img :src="$withBase('/img/12.png')">

## Estructura y Ejemplos

La estuctura del Objeto [Query](https://training.genexus.com/es/aprendiendo/pdf/disenando-consultas-dinamicas-objeto-query-pdf-6098967) son consultas las cuales pueden generar diferentes tipos de graficos algo como los conocidos [chartjs](https://www.chartjs.org/) la podemos observar al crear uno nuevo cuenta con 

* `Atributos`
* `Parametros`
* `Filtes(AND)`
* `OrderBY`

<img :src="$withBase('/img/13.png')">

Teniendo la siguiente asignacion del  Objeto [Query](https://training.genexus.com/es/aprendiendo/pdf/disenando-consultas-dinamicas-objeto-query-pdf-6098967) son consultas las cuales pueden generar diferentes tipos de graficos algo como los conocidos [chartjs](https://www.chartjs.org/) 

<img :src="$withBase('/img/14.png')">

```GeneXus
    Atributes
        * CityName
        * CountryName
        + Count(AttrationName)
    @@Parameters
        ## Aqui podemos ingresar parametros que requiera la consulta en base al cliente es decir un datos (IN)
    Filters (AND)
        CountryName = 'France'
    OrderBy
        CityName    
```
Bien. Ya hemos terminado de definir nuestra consulta. ¿Cómo ser verá el resultado?
Vayamos a la solapa Preview.


<img :src="$withBase('/img/15.png')">

Editando la propiedad Type, bajo el grupo Output podemos especificar una de las tres formas
de ver la salida. Elegimos Chart:

<img :src="$withBase('/img/16.png')">

## Aportes Bantotal y Concluciones

El objeto Query nos permite crear estas consultas de una forma simple e intuitiva,
aumentando el valor de la información obtenida de la base de datos

En muchas ocasiones necesitamos realizar consultas a la base de datos para analizar la
información y poder tomar decisiones.





