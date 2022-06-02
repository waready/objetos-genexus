# Data Selector

<!-- ## Browser API Access Restrictions

Because VuePress applications are server-rendered in Node.js when generating static builds, any Vue usage must conform to the [universal code requirements](https://ssr.vuejs.org/en/universal.html). In short, make sure to only access Browser / DOM APIs in `beforeMount` or `mounted` hooks.

If you are using or demoing components that are not SSR friendly (for example containing custom directives), you can wrap them inside the built-in `<ClientOnly>` component:

## -->

Los Data Selectors pueden ser utilizados en varios objetos. La forma de usarlos es conceptualmente igual en todos lados aunque varía levemente la forma, dependiendo de si el objeto que lo usa tiene o no código asociado. En los que tienen código, como los procedimientos, se utiliza la cláusula USING DataSelectorName(). En los que no lo tienen, como puede ser un Grid, se referencian utilizando la [propiedad Data Selecto](https://wiki.genexus.com/commwiki/servlet/wiki?5361,Data+Selector+property) en la que se especifica el DS y sus parámetros. Ver también [Data Selectors en Agregaciones](https://wiki.genexus.com/commwiki/servlet/wiki?5362,Data+Selectors+en+Agregaciones), y [Data Selectors in Grids](https://wiki.genexus.com/commwiki/servlet/wiki?5386,Data+Selectors+in+Grids).

## Funcionalidad Gx

Su funcionalidad es crear algunas sub consultas o filtros que se necesiten a un consulta en un `For Each`. Como sabemos para hacer un tipo de consulta a la `BD` y recorrer `transacciones` o (tablas) usamos `For Each` en el cual podemos definir los filtros que requieren usar con `Where` el puede ser remplazado con un `Data Selector` tal como veremos a continuación.

<img :src="$withBase('/img/05.png')">

Código que referencia al Data Selector ActiveCustomers

```GeneXus
    For each USING ActiveCustomers()
        &x = CustomerName
        ...
    EndFor
```

El resultado de la navegación es exactamente el mismo que si se hubiera especificado el siguiente código:

```GeneXus
    For each Where CustomerStatus = "Active"
       &x = CustomerName
       ...
    EndFor
```

## Estructura y Ejemplos

1- La definición del concepto "reciente" puede variar en el tiempo. Hoy puede referirse a lo que ocurrió en los últimos 5 días pero en algún momento puede cambiarse a 10, a 1, etc. Este DS tiene como objetivo encapsular el concepto mencionado de forma que cambiarlo implica sólo modificar el DS.

<img :src="$withBase('/img/06.png')">

Código que referencia al Data Selector anterior:

```GeneXus
    For each USING CustomersRecentlyChanged( &Today)
       &x = CustomerAddress
       ...
    EndFor
```

El resultado de la navegación es exactamente el mismo que si se hubiera especificado el siguiente código:

```GeneXus
    For each
    Order (CustomerLastUpdate)
    Where CustomerLastUpdate >= &Today - 5; // 5 days befor reference date
    Where CustomerLastUpdate <= &Today
       &x = CustomerAddress
       ...
    EndFor
```

2- La versatilidad de este objeto le permite anidar otros Data Selectors para aprovechar la navegación de éstos, a la vez que pueden ser reutilizados en forma independiente por cualquier otro Procedimiento donde sea necesario aplicarla. Tal es el caso del siguiente ejemplo, donde se desean listar todos los registros de África que tengan acceso a las costas oceánicas.

<img :src="$withBase('/img/07.png')">

La solución a la realidad implica que el DS AfricanOceanCities esté anidado en el otro. Esto se logra incluyendo el nombre del DS padre en la propiedad DataSelector.

<img :src="$withBase('/img/08.png')">

Código que referencia al Data Selector AfricanOceanCities:

```GeneXus
    For each using AfricanOceanCities()  
        Print AfricanOceanCities
    EndFor
```

El resultado de la navegación es exactamente el mismo que si se hubiera especificado el siguiente código:

```GeneXus
    For each
    where CountryWorldRegion = 5
    where CityOceanAccess = "Y"
        Print AfricanOceanCities
    Endfor
```

## Aportes Bantotal y Concluciones

El aporte seria muy grande por que En `Bantotal` se usan muchos filtros puesto que exiten varias llaves foreaneas para hacer un filtro adecuado a una tabla y la reduccion de codigo con el uso de los nombres de los `Data Selector` tendriamos una mejor documentacion y orden en el codigo referente a grandes filtros que se tienen algunas tablas.

<img :src="$withBase('/img/09.png')">

en `Condition` tendriamos lo siguiente:

```GeneXus
    FSD016_Filter = &Ppgcod
    FSD016_Filter = &Pitsuc
    FSD016_Filter = &Pitmod
    FSD016_Filter = &Pittran
    FSD016_Filter = &Pitnrel
    FSD016_Filter = &OrdAct
    FSD016_Filter < &Pitord
    FSD016_Filter <> 'S'    
```
Código que referencia al Data Selector FSD016_Filter:

```GeneXus
    For each using FSD016_Filter()  
      ...
    EndFor
```
