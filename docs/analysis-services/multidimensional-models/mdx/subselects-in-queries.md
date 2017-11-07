---
title: Subselecciones en las consultas | Documentos de Microsoft
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9e361798-688e-4b11-9eef-31fc793e8ba4
caps.latest.revision: 5
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 918c7727a7af1f85f93d110652da450f1ea770cb
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="subselects-in-queries"></a>Subselecciones en las consultas
  Las expresiones de subselección son expresiones SELECT anidadas que se utilizan para restringir el espacio del cubo donde se evalúa la instrucción SELECT externa exterior. Las subselecciones permiten definir un nuevo espacio en el que se evalúan todos los cálculos.  
  
## <a name="subselects-by-example"></a>Ejemplo de subselecciones  
 Comencemos con un ejemplo de cómo pueden ayudar las subselecciones a generar los resultados que deseamos mostrar. Suponga que le solicitan que genere una tabla que muestra el comportamiento de las ventas, a través de varios años, de los diez productos más vendidos.  
  
 El resultado debería ser similar al de la tabla siguiente:  
  
|||||  
|-|-|-|-|  
||Suma de años|Año 1|...|  
|Suma de los 10 productos más vendidos||||  
|Producto A||||  
|...||||  
  
 Para hacer algo como lo anterior, podría escribir la siguiente expresión MDX:  
  
```  
SELECT [Date].[Calendar Year].MEMBERS on 0  
     , TOPCOUNT( [Product].[Product].MEMBERS  
               , 10  
               , [Measures].[Sales Amount]  
               ) ON 1  
  FROM [Adventure Works]  
```  
  
 Devuelve los siguientes resultados:  
  
|||||||  
|-|-|-|-|-|-|  
||All Periods|CY 2005|CY 20062|CY 2007|CY 2008|  
|All Products|$80,450,596.98|$8,065,435.31|$24,144,429.65|$32,202,669.43|$16,038,062.60|  
|Mountain-200 Black, 38|$1,634,647.94|(null)|(null)|$894,207.97|$740,439.97|  
|Mountain-200 Black, 42|$1,285,524.65|(null)|(null)|$722,137.65|$563,387.00|  
|Mountain-200 Silver, 38|$1,181,945.82|(null)|(null)|$634,600.78|$547,345.03|  
|Mountain-200 Black, 46|$995,927.43|(null)|(null)|$514,995.76|$480,931.68|  
|Mountain-200 Silver, 42|$1,005,111.77|(null)|(null)|$529,543.29|$475,568.49|  
|Mountain-200 Silver, 46|$975,932.56|(null)|(null)|$526,759.30|$449,173.26|  
|Road-150 Red, 56|$792,228.98|$382,159.24|$410,069.74|(null)|(null)|  
|Mountain-200 Black, 38|$1,471,078.72|(null)|$789,958.49|$681,120.23|(null)|  
|Road-350-W Yellow, 48|$1,380,253.88|(null)|(null)|$744,988.37|$635,265.50|  
  
 Esto está muy cerca de lo que estamos buscando, excepto en que la consulta no devolvió diez productos sino nueve, y el total de productos no refleja la suma de todos los productos ni la de los nueve más vendidos (en este caso). Otro intento de resolver el problema se presenta en la siguiente consulta MDX:  
  
```  
SELECT [Date].[Calendar Year].MEMBERS on 0  
     , TOPCOUNT( [Product].[Product].CHILDREN, 10, [Measures].[Sales Amount]) ON 1  
  FROM [Adventure Works]  
```  
  
 Devuelve los siguientes resultados:  
  
|||||||  
|-|-|-|-|-|-|  
||All Periods|CY 2005|CY 2006|CY 2007|CY 2008|  
|Mountain-200 Black, 38|$1,634,647.94|(null)|(null)|$894,207.97|$740,439.97|  
|Mountain-200 Black, 42|$1,285,524.65|(null)|(null)|$722,137.65|$563,387.00|  
|Mountain-200 Silver, 38|$1,181,945.82|(null)|(null)|$634,600.78|$547,345.03|  
|Mountain-200 Black, 46|$995,927.43|(null)|(null)|$514,995.76|$480,931.68|  
|Mountain-200 Silver, 42|$1,005,111.77|(null)|(null)|$529,543.29|$475,568.49|  
|Mountain-200 Silver, 46|$975,932.56|(null)|(null)|$526,759.30|$449,173.26|  
|Road-150 Red, 56|$792,228.98|$382,159.24|$410,069.74|(null)|(null)|  
|Mountain-200 Black, 38|$1,471,078.72|(null)|$789,958.49|$681,120.23|(null)|  
|Road-350-W Yellow, 48|$1,380,253.88|(null)|(null)|$744,988.37|$635,265.50|  
|Road-150 Red, 62|$566,797.97|$234,018.86|$332,779.11|(null)|(null)|  
  
 Eso estaba muy cerca del resultado deseado porque solo faltó la suma de los productos. En este punto, se puede empezar a ajustar la expresión MDX anterior para agregar la línea que falta; sin embargo, esa tarea podría resultar complicada.  
  
 Otro enfoque para resolver el problema sería empezar a pensar en redefinir el espacio del cubo sobre el que se resuelve la expresión MDX. ¿Qué ocurre si el "nuevo" cubo solo contiene los datos de los diez productos más vendidos? Ese cubo tendrá entonces el miembro All ajustado a los diez productos únicamente y una simple consulta resolvería las necesidades.  
  
 La siguiente expresión MDX utiliza una instrucción de subselección para volver a definir el espacio del cubo para los diez productos más vendidos y generar los resultados deseados:  
  
```  
SELECT [Date].[Calendar Year].MEMBERS on 0  
     , [Product].[Product].MEMBERS on 1  
  FROM (SELECT TOPCOUNT( [Product].[Product].CHILDREN  
                       , 10  
                       , [Measures].[Sales Amount]  
                       ) ON 0  
          FROM [Adventure Works]  
        )  
 WHERE [Measures].[Sales Amount]  
```  
  
 La expresión anterior devuelve los siguientes resultados:  
  
|||||||  
|-|-|-|-|-|-|  
||All Periods|CY 2005|CY 2006|CY 2007|CY 2008|  
|All Products|$19,997,183.30|$1,696,815.63|$2,816,611.28|$7,930,797.72|$7,552,958.66|  
|Mountain-200 Silver, 38|$2,160,981.60|(null)|(null)|$1,024,359.10|$1,136,622.49|  
|Mountain-200 Silver, 42|$1,914,547.85|(null)|(null)|$903,061.68|$1,011,486.18|  
|Mountain-200 Silver, 46|$1,906,248.55|(null)|(null)|$877,077.79|$1,029,170.76|  
|Mountain-200 Black, 38|$1,811,229.02|(null)|$896,511.60|$914,717.43|(null)|  
|Mountain-200 Black, 38|$2,589,363.78|(null)|(null)|$1,261,406.37|$1,327,957.41|  
|Mountain-200 Black, 42|$2,265,485.38|(null)|(null)|$1,126,055.89|$1,139,429.49|  
|Mountain-200 Black, 46|$1,957,528.24|(null)|(null)|$946,453.88|$1,011,074.37|  
|Road-150 Red, 62|$1,769,096.69|$828,011.68|$941,085.01|(null)|(null)|  
|Road-150 Red, 56|$1,847,818.63|$868,803.96|$979,014.67|(null)|(null)|  
|Road-350-W Yellow, 48|$1,774,883.56|(null)|(null)|$877,665.59|$897,217.96|  
  
 Los resultados anteriores son exactamente los que estábamos buscando.  
  
 Revisemos lo que hacía exactamente la subselección. Devolvía un nuevo cubo que contenía todas las demás dimensiones del producto tal cual; pero, en la dimensión de producto, filtraba todos los miembros para coincidir con los diez productos principales que nos interesaban, como si hubiéramos quitado todos los datos que no cumplieran los criterios de los diez más vendidos y se hubiera vuelto a crear el cubo. El otro concepto importante de entender en este ejemplo es el hecho de que los diez productos más vendidos se calculaban sobre el miembro All de todas las otras dimensiones del cubo; lo anterior es cierto porque ninguna otra restricción de filtrado se impuso en la subselección.  
  
 Las subselecciones pueden ser tan complejas como se desee; el siguiente ejemplo mostrará cómo generar una tabla similar a la mencionada antes, pero filtrada con France en la dimensión Sales Territory y con Internet en la dimensión Sales Channel.  
  
```  
SELECT [Date].[Calendar Year].MEMBERS on 0  
     , [Product].[Product].MEMBERS on 1  
  FROM (SELECT TOPCOUNT( [Product].[Product].CHILDREN  
                       , 10  
                       , [Measures].[Sales Amount]  
                       ) ON 0  
             , [Sales Territory].[Sales Territory].[Region].[France] on 1  
             ,  [Sales Channel].[Sales Channel].[Internet] on 2  
          FROM [Adventure Works]  
        )  
 WHERE [Measures].[Sales Amount]  
```  
  
 Se produjeron los siguientes resultados:  
  
|||||||  
|-|-|-|-|-|-|  
||All Periods|CY 2005|CY 2006|CY 2007|CY 2008|  
|All Products|$748,682.49|$32,204.43|$73,125.18|$269,506.56|$373,846.32|  
|Mountain-200 Silver, 38|$90,479.61|(null)|(null)|$41,759.82|$48,719.79|  
|Mountain-200 Silver, 42|$97,439.58|(null)|(null)|$39,439.83|$57,999.75|  
|Mountain-200 Silver, 46|$102,079.56|(null)|(null)|$27,839.88|$74,239.68|  
|Mountain-200 Black, 38|$26,638.28|(null)|$12,294.59|$14,343.69|(null)|  
|Mountain-200 Black, 38|$96,389.58|(null)|(null)|$41,309.82|$55,079.76|  
|Mountain-200 Black, 42|$80,324.65|(null)|(null)|$43,604.81|$36,719.84|  
|Mountain-200 Black, 46|$107,864.53|(null)|(null)|$45,899.80|$61,964.73|  
|Road-150 Red, 62|$46,517.51|$14,313.08|$32,204.43|(null)|(null)|  
|Road-150 Red, 56|$46,517.51|$17,891.35|$28,626.16|(null)|(null)|  
|Road-350-W Yellow, 48|$54,431.68|(null)|(null)|$15,308.91|$39,122.77|  
  
 Los resultados anteriores son los diez productos principales vendidos en Francia a través del canal de Internet.  
  
## <a name="subselect-statement"></a>Instrucción de subselección  
 El BNF de la subselección es:  
  
```  
[WITH [<calc-clause> ...]]  
SELECT [<axis-spec> [, <axis-spec> ...]]  
FROM [<identifier> | (< sub-select-statement >)]  
[WHERE <slicer>]  
[[CELL] PROPERTIES <cellprop> [, <cellprop> ...]]  
  
< sub-select-statement > :=  
   SELECT [<axis-spec> [, <axis-spec> ...]]  
   FROM [<identifier> | (< sub-select-statement >)]  
   [WHERE <slicer>]  
  
```  
  
 La subselección es otra instrucción Select donde las especificaciones del eje y la especificación de la segmentación filtran el espacio del cubo sobre el que se evalúa la selección exterior.  
  
 Cuando a continuación se especifica un miembro en el eje o la cláusula de la segmentación, ese miembro con sus ascendientes y descendientes se incluye en el espacio del subcubo para la subselección; todos los miembros relacionados no mencionados, en el eje o en la cláusula de la segmentación, y sus descendientes se filtran del subespacio. De esta manera, el espacio de la selección exterior se ha limitado a los miembros existentes en la cláusula de eje o en la cláusula de la segmentación, con sus ascendientes y descendientes, tal y como se mencionó antes.  
  
 Dado que el miembro All de todas las dimensiones no mencionadas en el eje o en las cláusulas de la segmentación pertenecen al espacio de la selección; todos los descendientes del miembro All en esas dimensiones son también parte del espacio de la subselección.  
  
 El miembro All, en todas las dimensiones, del espacio del subcubo se vuelve a evaluar para reflejar el efecto de las restricciones del nuevo espacio.  
  
 En el siguiente ejemplo se mostrará lo que se ha dicho anteriormente; la primera expresión MDX ayuda a mostrar los valores sin filtrar en el cubo, la segunda muestra el efecto de filtrar en la cláusula de subselección:  
  
```  
SELECT { [Customer].[Customer Geography].[All Customers]  
       , [Customer].[Customer Geography].[Country].&[United States]  
       , [Customer].[Customer Geography].[State-Province].&[OR]&[US]  
       , [Customer].[Customer Geography].[City].&[Portland]&[OR]  
       , [Customer].[Customer Geography].[State-Province].&[WA]&[US]  
       , [Customer].[Customer Geography].[City].&[Seattle]&[WA]  
       } ON 1  
     ,  {[Measures].[Internet Sales Amount], [Measures].[Reseller Sales Amount]} ON 0  
  FROM [Adventure Works]  
```  
  
 Devuelve los siguientes valores:  
  
||||  
|-|-|-|  
||Internet Sales Amount|Reseller Sales Amount|  
|All Customers|$29,358,677.22|$80,450,596.98|  
|United States|$9,389,789.51|$80,450,596.98|  
|Oregon|$1,170,991.54|$80,450,596.98|  
|Portland|$110,649.54|$80,450,596.98|  
|Washington|$2,467,248.34|$80,450,596.98|  
|Seattle|$75,164.86|$80,450,596.98|  
  
 En el ejemplo anterior, Seattle es un elemento secundario de Washington, Portland es un elemento secundario de Oregon, Oregon y Washington son elementos secundarios de Estados Unidos, y Estados Unidos es un elemento secundario de [Customer Geography].[All Customers]. Todos los miembros mostrados en este ejemplo tienen otros elementos relacionados que contribuyen al valor agregado primario; es decir, Spokane, Tacoma y Everett son ciudades relacionadas de Seattle y todas contribuyen a Washington Internet Sales Amount. El valor de Reseller Sales Amount es independiente del atributo Customer Geography; por lo tanto, el valor All se muestra en los resultados. La expresión MDX siguiente muestra el efecto del filtrado de la cláusula de subselección:  
  
```  
SELECT { [Customer].[Customer Geography].[All Customers]  
       , [Customer].[Customer Geography].[Country].&[United States]  
       , [Customer].[Customer Geography].[State-Province].&[OR]&[US]  
       , [Customer].[Customer Geography].[City].&[Portland]&[OR]  
       , [Customer].[Customer Geography].[State-Province].&[WA]&[US]  
       , [Customer].[Customer Geography].[City].&[Seattle]&[WA]  
       } ON 1  
     ,  {[Measures].[Internet Sales Amount], [Measures].[Reseller Sales Amount]} ON 0  
  FROM ( SELECT [Customer].[State-Province].&[WA]&[US] ON 0  
           FROM [Adventure Works]  
        )  
```  
  
 Devuelve los siguientes valores:  
  
||||  
|-|-|-|  
||Internet Sales Amount|Reseller Sales Amount|  
|All Customers|$2,467,248.34|$80,450,596.98|  
|United States|$2,467,248.34|$80,450,596.98|  
|Washington|$2,467,248.34|$80,450,596.98|  
|Seattle|$75,164.86|$80,450,596.98|  
  
 Los resultados anteriores muestran que solo los ascendientes y los descendientes de Washington State forman parte del subespacio donde se evalúa la instrucción de selección exterior; Oregon y Portland se han quitado del subcubo porque Oregon y todos los demás estados relacionados no se mencionaron en la subselección al mismo tiempo que Washington.  
  
 El miembro All se ajustó para reflejar el filtrado en Washington; no solo se ajustó en la dimensión [Customer Geography] sino en todas las demás dimensiones que se cruzaron con ella. Todas las dimensiones que no se cruzan con [Customer Geography] permanecen en el subcubo inalteradas.  
  
 Las siguientes dos instrucciones MDX ilustran cómo se ajusta el miembro All en otras dimensiones para cumplir el efecto de filtrado de la subselección. La primera consulta muestra los resultados inalterados y la segunda el efecto del filtrado:  
  
```  
SELECT { [Customer].[Customer Geography].[All Customers]  
       , [Customer].[Customer Geography].[Country].&[United States]  
       , [Customer].[Customer Geography].[State-Province].&[OR]&[US]  
       , [Customer].[Customer Geography].[City].&[Portland]&[OR]  
       , [Customer].[Customer Geography].[State-Province].&[WA]&[US]  
       , [Customer].[Customer Geography].[City].&[Seattle]&[WA]  
       } ON 1  
     ,   [Product].[Product Line].MEMBERS ON 0  
  FROM [Adventure Works]  
 WHERE [Measures].[Internet Sales Amount]  
```  
  
||||||||  
|-|-|-|-|-|-|-|  
||All Products|Accessory|Components|Mountain|Road|Touring|  
|All Customers|$29,358,677.22|$604,053.30|(null)|$10,251,183.52|$14,624,108.58|$3,879,331.82|  
|United States|$9,389,789.51|$217,168.79|(null)|$3,547,956.78|$4,322,438.41|$1,302,225.54|  
|Oregon|$1,170,991.54|$30,513.17|(null)|$443,607.98|$565,372.10|$131,498.29|  
|Portland|$110,649.54|$2,834.17|(null)|$47,099.91|$53,917.17|$6,798.29|  
|Washington|$2,467,248.34|$62,662.92|(null)|$945,219.38|$1,155,880.07|$303,485.97|  
|Seattle|$75,164.86|$2,695.74|(null)|$19,914.53|$44,820.06|$7,734.54|  
  
```  
SELECT { [Customer].[Customer Geography].[All Customers]  
       , [Customer].[Customer Geography].[Country].&[United States]  
       , [Customer].[Customer Geography].[State-Province].&[OR]&[US]  
       , [Customer].[Customer Geography].[City].&[Portland]&[OR]  
       , [Customer].[Customer Geography].[State-Province].&[WA]&[US]  
       , [Customer].[Customer Geography].[City].&[Seattle]&[WA]  
       } ON 1  
     ,   [Product].[Product Line].MEMBERS ON 0  
  FROM ( SELECT [Customer].[State-Province].&[WA]&[US] ON 0  
           FROM [Adventure Works]  
        )  
 WHERE [Measures].[Internet Sales Amount]  
```  
  
||||||||  
|-|-|-|-|-|-|-|  
||All Products|Accessory|Components|Mountain|Road|Touring|  
|All Customers|$2,467,248.34|$62,662.92|(null)|$945,219.38|$1,155,880.07|$303,485.97|  
|United States|$2,467,248.34|$62,662.92|(null)|$945,219.38|$1,155,880.07|$303,485.97|  
|Washington|$2,467,248.34|$62,662.92|(null)|$945,219.38|$1,155,880.07|$303,485.97|  
|Seattle|$75,164.86|$2,695.74|(null)|$19,914.53|$44,820.06|$7,734.54|  
  
 Los resultados anteriores muestran que los valores de All Products se han ajustado a los valores de Washington State únicamente, tal y como se esperaba.  
  
 Las subselecciones se pueden anidar sin límite en la profundidad, excepto por la memoria disponible. La subselección interna define el subespacio inicial sobre el que se aplica el filtrado y se pasa a la siguiente selección exterior. Una cuestión importante que tener en cuenta es el hecho de que el anidamiento no es una operación conmutativa, de modo que el orden en el que el se establece hace que se produzcan resultados diferentes. Los siguientes ejemplos deberían mostrar la diferencia al elegir un orden de anidamiento.  
  
```  
SELECT [Sales Territory].[Sales Territory Region].MEMBERS on 0  
     , [Product].[Product].MEMBERS on 1  
  FROM (SELECT TOPCOUNT( [Product].[Product].CHILDREN, 5, [Measures].[Sales Amount]) ON 0  
          FROM (SELECT TOPCOUNT( [Sales Territory].[Sales Territory Region].CHILDREN, 5, [Measures].[Sales Amount]) on 0  
                  FROM [Adventure Works]  
               )  
        )  
 WHERE [Measures].[Sales Amount]  
```  
  
 Se devuelven los siguientes resultados.  
  
||||||||  
|-|-|-|-|-|-|-|  
||All Sales Territories|Australia|Canada|Central|Northwest|Southwest|  
|All Products|$7,591,495.49|$1,281,059.99|$1,547,298.12|$600,205.79|$1,924,763.50|$2,238,168.08|  
|Mountain-200 Silver, 38|$1,449,576.15|$248,702.93|$275,052.45|$141,103.65|$349,487.01|$435,230.12|  
|Mountain-200 Black, 38|$1,722,896.50|$218,024.05|$418,726.43|$123,929.46|$486,694.63|$475,521.93|  
|Mountain-200 Black, 42|$1,573,655.14|$239,137.96|$319,921.61|$130,102.75|$420,445.84|$464,046.98|  
|Mountain-200 Black, 46|$1,420,500.58|$192,320.16|$230,875.99|$117,044.49|$424,813.66|$455,446.27|  
|Road-150 Red, 56|$1,424,867.11|$382,874.89|$302,721.64|$88,025.44|$243,322.36|$407,922.78|  
  
```  
SELECT [Sales Territory].[Sales Territory Region].MEMBERS on 0  
     , [Product].[Product].MEMBERS on 1  
  FROM (SELECT TOPCOUNT( [Sales Territory].[Sales Territory Region].CHILDREN, 5, [Measures].[Sales Amount]) ON 0  
          FROM (SELECT TOPCOUNT( [Product].[Product].CHILDREN, 5, [Measures].[Sales Amount]) on 0  
                  FROM [Adventure Works]  
               )  
        )  
 WHERE [Measures].[Sales Amount]  
```  
  
 Se devuelven los siguientes resultados.  
  
||||||||  
|-|-|-|-|-|-|-|  
||All Sales Territories|Australia|Canada|Northwest|Southwest|United Kingdom|  
|All Products|$7,938,218.56|$1,096,312.24|$1,474,255.49|$2,042,674.72|$2,238,099.55|$1,086,876.56|  
|Mountain-200 Silver, 38|$1,520,958.53|$248,702.93|$275,052.45|$349,487.01|$435,230.12|$212,486.03|  
|Mountain-200 Silver, 42|$1,392,237.14|$198,127.15|$229,679.01|$361,233.58|$407,854.24|$195,343.16|  
|Mountain-200 Black, 38|$1,861,703.23|$218,024.05|$418,726.43|$486,694.63|$475,521.93|$262,736.19|  
|Mountain-200 Black, 42|$1,702,427.25|$239,137.96|$319,921.61|$420,445.84|$464,046.98|$258,874.87|  
|Mountain-200 Black, 46|$1,460,892.41|$192,320.16|$230,875.99|$424,813.66|$455,446.27|$157,436.31|  
  
 Como puede ver, hay diferencias en los resultados entre ambos conjuntos. La primera consulta respondía a la pregunta de cuáles son los productos que más se venden en las cinco regiones de mayores ventas; la segunda consulta respondía a la pregunta de dónde se producen las ventas más importantes de los cinco productos que más se venden.  
  
### <a name="remarks"></a>Comentarios  
 Las subselecciones tienen las siguientes restricciones y limitaciones:  
  
-   La cláusula WHERE no filtra el subespacio.  
  
-   La cláusula WHERE solo cambia el miembro predeterminado en el subcubo.  
  
-   La cláusula NON EMPTY no se permite en una cláusula de eje; use una expresión de la función [NonEmpty &#40;MDX&#41;](../../../mdx/nonempty-mdx.md) en su lugar.  
  
-   La cláusula HAVING no se permite en una cláusula de eje; use una expresión de la función [Filter &#40;MDX&#41;](../../../mdx/filter-mdx.md) en su lugar.  
  
-   De forma predeterminada, los miembros calculados no se permiten en subselecciones; Sin embargo, esta restricción se puede cambiar, en una base por cada sesión, asignando un valor a la **subconsultas** propiedad de cadena de conexión en <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A> o **DBPROP_MSMD_SUBQUERIES** propiedad en [ Propiedades XMLA compatibles &#40; XMLA &#41; ](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md). Vea [Miembros calculados en subselecciones y subcubos](../../../analysis-services/multidimensional-models/mdx/calculated-members-in-subselects-and-subcubes.md) para obtener una explicación detallada del comportamiento de los miembros calculados según los valores de **SubQueries** o **DBPROP_MSMD_SUBQUERIES**.  
  
  

