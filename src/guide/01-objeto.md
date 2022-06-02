# Data Provider

<!-- ## Browser API Access Restrictions

Because VuePress applications are server-rendered in Node.js when generating static builds, any Vue usage must conform to the [universal code requirements](https://ssr.vuejs.org/en/universal.html). In short, make sure to only access Browser / DOM APIs in `beforeMount` or `mounted` hooks.

If you are using or demoing components that are not SSR friendly (for example containing custom directives), you can wrap them inside the built-in `<ClientOnly>` component:

## -->

El propósito de los Data Providers es obtener información jerárquica para que quien la necesita pueda luego hacer algo con ella. Recordemos que en los Data Providers el foco está ubicado en el lenguaje de salida: se indica en una estructura jerárquica cómo se compone ese output. Por eso se habla de un proceso de transformación de los datos de entrada en esa salida estructurada. Datos que pueden ser de la base de datos o no.

La manera de representar estructuras jerárquicas en GeneXus es con el objeto [SDT](http://library.gxtechnical.com/gxdlsp/dist/GeneXus/DevEnv/Docum/ReleaseNotes/8.0/StructureDatatype.htm#:~:text=El%20objeto%20GeneXus%20Structured%20Data,facilita%20y%20potencia%20la%20programaci%C3%B3n.), junto con la posibilidad de definir colecciones. Por supuesto, un Business Component puede pensarse estructuralmente como un [SDT](http://library.gxtechnical.com/gxdlsp/dist/GeneXus/DevEnv/Docum/ReleaseNotes/8.0/StructureDatatype.htm#:~:text=El%20objeto%20GeneXus%20Structured%20Data,facilita%20y%20potencia%20la%20programaci%C3%B3n.). Es por ello que en la propiedad Output del Data Provider podremos especificar tanto un [SDT](http://library.gxtechnical.com/gxdlsp/dist/GeneXus/DevEnv/Docum/ReleaseNotes/8.0/StructureDatatype.htm#:~:text=El%20objeto%20GeneXus%20Structured%20Data,facilita%20y%20potencia%20la%20programaci%C3%B3n.) como un Business Component. Y además tenemos la propiedad Collection para poder indicar que la salida será una colección de ese tipo de datos indicado, o no, o será un único ítem.

## Funcionalidad Gx

De modo que un Data Provider siempre devolverá a quien lo llame una jerarquía, ya sea un [SDT](http://library.gxtechnical.com/gxdlsp/dist/GeneXus/DevEnv/Docum/ReleaseNotes/8.0/StructureDatatype.htm#:~:text=El%20objeto%20GeneXus%20Structured%20Data,facilita%20y%20potencia%20la%20programaci%C3%B3n.), una colección de [SDT](http://library.gxtechnical.com/gxdlsp/dist/GeneXus/DevEnv/Docum/ReleaseNotes/8.0/StructureDatatype.htm#:~:text=El%20objeto%20GeneXus%20Structured%20Data,facilita%20y%20potencia%20la%20programaci%C3%B3n.), un Business Component, o una colección de Business Components.

<img :src="$withBase('/img/01.png')">
<img :src="$withBase('/img/02.png')">

Aquí vemos cómo GeneXus ofrece diferentes métodos de conversión entre SDTs y algunos de esos otros formatos. Si en el futuro aparece un nuevo formato de representación de información estructurada, el Data Provider continuará invariable. GeneXus implementará el método de transformación a ese formato, y solo habrá que utilizarlo. Podemos tanto convertir de SDT a otro formato, como a la inversa: de ese otro formato a SDT. Esto ya no tiene que ver con el Data Provider en si, sino con los tipos de datos estructurados. El obtener la colección de países podría haberse logrado con un procedimiento en lugar de un Data Provider, y la parte de la conversión sería idéntica.

## Estructura y Ejemplos

Veamos este ejemplo. Supongamos que, en el contexto de una aplicación para una agencia de viajes, necesitamos mostrar en pantalla un ranking de países, ordenados de mayor a menor por cantidad de atracciones turísticas para visitar que cada uno tiene. En nuestra realidad tenemos las transacciones Country y Attraction con los siguientes atributos. Una forma sencilla de conseguirlo es declarar un Data Provider que devuelva una colección de países donde para cada uno se agregue, además de su nombre e identificador, la cantidad de atracciones que posee. Y luego procesar esa colección en orden inverso por esa cantidad. Como dijimos, el lenguaje del Data Provider coloca el foco en la salida, se calculan los elementos desde el punto de vista de la jerarquía que resultará.

<img :src="$withBase('/img/03.png')">
Para representar este ejemplo, creamos la siguiente estructura de datos
que será la que posteriormente devuelva el Data Provider. Y luego
debemos cargar este objeto SDT dentro del Source del Data Provider

```GeneXus
    Countries
    {
        CountriesItem
        {
            Id = /*Id Value*/
            Name = /*Name Value*/
            AttractionsQuantity = /*Attractions Quantity value*/
        }
    }
```
-------------------------------------------------------------------------------------------------------------------------------
```GeneXus
    Countries
    {
        CountriesItem
        {
            Id = CountryId
            Name = CountryName
            AttractionsQuantity = count(AttractionName)
        }
    }
```


Al arrastrar dentro de él el SDT que será el output del Data Provider, ya nos
presenta la estructura que tenemos que cargar. Vemos claramente cómo
su lenguaje está orientado hacia la declaración de salida

<img :src="$withBase('/img/04.png')">

## Aportes Bantotal y Concluciones

Basandonos en datos [SDT](http://library.gxtechnical.com/gxdlsp/dist/GeneXus/DevEnv/Docum/ReleaseNotes/8.0/StructureDatatype.htm#:~:text=El%20objeto%20GeneXus%20Structured%20Data,facilita%20y%20potencia%20la%20programaci%C3%B3n.), tendriamos una Programacion mas orientada a Objetos pudiendo remplazar otro tipo de objetos que se usan frecuentemente como `array o vectores` a los cuales haciamos un recorrido para sacar los datos pre obtendios con un filtro los caules pueden ser remplazados por una funcion como `.sort()`, incluso podriamos usar otros tipos de parametros o funciones que nos proporciona los `Data Provider` como los siguientes:

* ```DataProvider.sort()```
* ```DataProvider.count()```
* ```DataProvider.Add(&Parametro)```
* ```DataProvider.remove(&index)```
* ```DataProvider.clear()```

Para tener mas conocimiento de esto pueden acceder a [Parametros](https://wiki.genexus.com/commwiki/servlet/wiki?6352,Collection%20variables).




