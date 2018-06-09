---
title: Instrucción SELECT (MDX) | Documentos de Microsoft
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 55a4e841a181e788892c293ec9c39a1a53a0459e
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34741894"
---
# <a name="mdx-data-manipulation---select"></a>Manipulación de datos MDX - SELECT


  Recupera datos de un cubo especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
[ WITH <SELECT WITH clause>   
   [ , <SELECT WITH clause>...n ]   
]   
SELECT   
     [ *   
    | ( <SELECT query axis clause>   
                  [ , <SELECT query axis clause>,...n ]   
            )   
            ]  
FROM   
   <SELECT subcube clause>   
      [ <SELECT slicer axis clause> ]  
      [ <SELECT cell property list clause> ]  
  
<SELECT WITH clause> ::=  
     ( CELL CALCULATION <CREATE CELL CALCULATION body clause> )   
   | ( [ CALCULATED ] MEMBER <CREATE MEMBER body clause>)   
   | ( SET <CREATE SET body clause>)  
   | ( MEASURE = <measure body clause> )  
  
<SELECT query axis clause> ::=  
   [ NON EMPTY ] Set_Expression  
   [ <SELECT dimension property list clause> ]   
      ON   
            Integer_Expression   
       | AXIS(Integer)   
       | COLUMNS   
       | ROWS   
       | PAGES   
       | SECTIONS   
       | CHAPTERS   
  
<SELECT subcube clause> ::=  
      Cube_Name   
   | [NON VISUAL] (SELECT   
                  [ *   
       | ( <SELECT query axis clause> [ ,   
           <SELECT query axis clause>,...n ] )   
         ]   
            FROM   
         <SELECT subcube clause>   
         <SELECT slicer axis clause> )  
  
<SELECT slicer axis clause> ::=   
      WHERE Tuple_Expression  
  
<SELECT cell property list clause> ::=   
   [ CELL ] PROPERTIES CellProperty_Name   
      [ , CellProperty_Name,...n ]  
  
<SELECT dimension property list clause> ::=  
   [DIMENSION] PROPERTIES   
      (DimensionProperty_Name   
         [,DimensionProperty_Name,...n ] )   
    | (LevelProperty_Name   
         [, LevelProperty_Name,...n ] )   
    | (MemberProperty_Name   
         [, MemberProperty_Name,...n ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Integer*  
 Entero entre 0 y 127.  
  
 *Restricciones obligatorias Cube_Name*  
 Cadena válida que proporciona un nombre de cubo.  
  
 *Tuple_Expression*  
 Expresión MDX válida que devuelve una tupla.  
  
 *CellProperty_Name*  
 Cadena válida que representa una propiedad de celda.  
  
 *DimensionProperty_Name*  
 Cadena válida que representa una propiedad de dimensión.  
  
 *LevelProperty_Name*  
 Cadena válida que representa una propiedad de nivel.  
  
 *MemberProperty_Name*  
 Cadena válida que representa una propiedad de miembro.  
  
## <a name="remarks"></a>Notas  
 La expresión `<SELECT slicer axis clause>` debe contener miembros en dimensiones y jerarquías distintas a las referidas en las expresiones `<SELECT query axis clause>` especificadas.  
  
 Si se omite un atributo del cubo de las expresiones `<SELECT query axis clause>` y del valor `<SELECT slicer axis clause>` especificados, el miembro predeterminado del atributo se agrega implícitamente al eje segmentador.  
  
 La opción NON VISUAL en la instrucción subselect le permite filtrar los miembros manteniendo los totales verdaderos en lugar de los totales filtrados. Esto le permite consultar las diez primeras ventas (personas/productos/regiones) y obtener el verdadero total de ventas para todos los miembros consultados, en lugar del valor total de ventas para los diez primeros devueltos. Para obtener más información, vea la sección de ejemplos.  
  
 Los miembros calculados pueden incluirse en \<cláusula de eje de consulta SELECT > cada vez que se abrió la conexión con el parámetro de cadena de conexión *subconsultas = 1*; vea [admite propiedades XMLA &#40; XMLA&#41; ](../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md) y <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A> para el uso de parámetros. Se proporciona un ejemplo de miembros calculados en subselecciones.  
  
## <a name="autoexists"></a>autoexist  
 Cuando dos o más atributos de la dimensión se utilizan en una instrucción SELECT, Analysis Services evalúa las expresiones de los atributos para asegurarse de que los miembros de dichos atributos están correctamente delimitados a fin de cumplir los criterios de todos los demás atributos. Por ejemplo, supongamos que está trabajando con atributos de la dimensión Geography. Si tiene una expresión que devuelve a todos los miembros del atributo City y otra expresión que delimita los miembros del atributo Country a todos los países de Europa, esto provocará en los miembros de City quedarán delimitados a solo aquellas ciudades que pertenezcan a países de Europa. Esta característica de Analysis Services se denomina Autoexists y solamente se aplica a atributos de una misma dimensión. Autoexists solamente se aplica a atributos de una misma dimensión porque intenta impedir que los registros de la dimensión excluidos de una expresión de atributos se incluyan en las demás expresiones de atributos. Autoexists también puede entenderse como la intersección resultante de las distintas expresiones de atributos sobre los registros de la dimensión. Vea los ejemplos que se muestran a continuación:  
  
 `//Obtain the Top 10 best reseller selling products by Name`  
  
 `with member [Measures].[PCT Discount] AS '[Measures].[Discount Amount]/[Measures].[Reseller Sales Amount]', FORMAT_STRING = 'Percent'`  
  
 `set Top10SellingProducts as 'topcount([Product].[Model Name].children, 10, [Measures].[Reseller Sales Amount])'`  
  
 `set Preferred10Products as '`  
  
 `{[Product].[Model Name].&[Mountain-200],`  
  
 `[Product].[Model Name].&[Road-250],`  
  
 `[Product].[Model Name].&[Mountain-100],`  
  
 `[Product].[Model Name].&[Road-650],`  
  
 `[Product].[Model Name].&[Touring-1000],`  
  
 `[Product].[Model Name].&[Road-550-W],`  
  
 `[Product].[Model Name].&[Road-350-W],`  
  
 `[Product].[Model Name].&[HL Mountain Frame],`  
  
 `[Product].[Model Name].&[Road-150],`  
  
 `[Product].[Model Name].&[Touring-3000]`  
  
 `}'`  
  
 `select {[Measures].[Reseller Sales Amount], [Measures].[Discount Amount], [Measures].[PCT Discount]} on 0,`  
  
 `Top10SellingProducts on 1`  
  
 `from [Adventure Works]`  
  
 El conjunto de resultados obtenido es el siguiente:  
  
|||||  
|-|-|-|-|  
||**Reseller Sales Amount**|**Discount Amount**|**PCT Discount**|  
|**Mountain-200**|**$14,356,699.36**|**$19,012.71**|**0,13 %**|  
|**Road-250**|**$9,377,457.68**|**$4,032.47**|**0.04%**|  
|**Mountain-100**|**$8,568,958.27**|**$139,393.27**|**1,63 %**|  
|**Road-650**|**$7,442,141.81**|**$39,698.30**|**0,53 %**|  
|**Touring-1000**|**$6,723,794.29**|**$166,144.17**|**2,47 %**|  
|**Road-550-W**|**$3,668,383.88**|**$1,901.97**|**0,05 %**|  
|**Road-350-W**|**$3,665,932.31**|**$20,946.50**|**0,57 %**|  
|**HL Mountain Frame**|**$3,365,069.27**|**$174.11**|**0,01 %**|  
|**Road-150**|**$2,363,805.16**|**$0.00**|**0.00%**|  
|**Touring-3000**|**$2,046,508.26**|**$79,582.15**|**3,89 %**|  
  
 El conjunto de productos obtenido parece el mismo que el de Preferred10Products; de modo que, comprobando el conjunto de Preferred10Products:  
  
 `with member [Measures].[PCT Discount] AS '[Measures].[Discount Amount]/[Measures].[Reseller Sales Amount]', FORMAT_STRING = 'Percent'`  
  
 `set Top10SellingProducts as 'topcount([Product].[Model Name].children, 10, [Measures].[Reseller Sales Amount])'`  
  
 `set Preferred10Products as '`  
  
 `{[Product].[Model Name].&[Mountain-200],`  
  
 `[Product].[Model Name].&[Road-250],`  
  
 `[Product].[Model Name].&[Mountain-100],`  
  
 `[Product].[Model Name].&[Road-650],`  
  
 `[Product].[Model Name].&[Touring-1000],`  
  
 `[Product].[Model Name].&[Road-550-W],`  
  
 `[Product].[Model Name].&[Road-350-W],`  
  
 `[Product].[Model Name].&[HL Mountain Frame],`  
  
 `[Product].[Model Name].&[Road-150],`  
  
 `[Product].[Model Name].&[Touring-3000]`  
  
 `}'`  
  
 `select {[Measures].[Reseller Sales Amount], [Measures].[Discount Amount], [Measures].[PCT Discount]} on 0,`  
  
 `Preferred10Products on 1`  
  
 `from [Adventure Works]`  
  
 En lo que respecta a los siguientes resultados, ambos conjuntos (Top10SellingProducts y Preferred10Products) son iguales.  
  
|||||  
|-|-|-|-|  
||**Reseller Sales Amount**|**Discount Amount**|**PCT Discount**|  
|**Mountain-200**|**$14,356,699.36**|**$19,012.71**|**0,13 %**|  
|**Road-250**|**$9,377,457.68**|**$4,032.47**|**0.04%**|  
|**Mountain-100**|**$8,568,958.27**|**$139,393.27**|**1,63 %**|  
|**Road-650**|**$7,442,141.81**|**$39,698.30**|**0,53 %**|  
|**Touring-1000**|**$6,723,794.29**|**$166,144.17**|**2,47 %**|  
|**Road-550-W**|**$3,668,383.88**|**$1,901.97**|**0,05 %**|  
|**Road-350-W**|**$3,665,932.31**|**$20,946.50**|**0,57 %**|  
|**HL Mountain Frame**|**$3,365,069.27**|**$174.11**|**0,01 %**|  
|**Road-150**|**$2,363,805.16**|**$0.00**|**0.00%**|  
|**Touring-3000**|**$2,046,508.26**|**$79,582.15**|**3,89 %**|  
  
 En los ejemplos anteriores hemos creado dos conjuntos: uno de ellos como una expresión calculada, y el otro como una expresión constante. Estos ejemplos ilustran los distintos tipos de Autoexists.  
  
 Autoexists puede aplicarse a las expresiones de modo profundo o superficial. El valor predeterminado es el modo profundo. En el siguiente ejemplo se ilustrará el concepto de Autoexists en modo profundo. En el ejemplo, Top10SellingProducts se filtra por el atributo [Product].[Product Line] para los productos del grupo [Mountain]. Tenga en cuenta que ambos atributos (slicer y axis) pertenecen a la misma dimensión, [Product].  
  
 `with member [Measures].[PCT Discount] AS '[Measures].[Discount Amount]/[Measures].[Reseller Sales Amount]', FORMAT_STRING = 'Percent'`  
  
 `set Top10SellingProducts as 'topcount([Product].[Model Name].children, 10, [Measures].[Reseller Sales Amount])'`  
  
 `// Preferred10Products set removed for clarity`  
  
 `select {[Measures].[Reseller Sales Amount], [Measures].[Discount Amount], [Measures].[PCT Discount]} on 0,`  
  
 `Top10SellingProducts on 1`  
  
 `from [Adventure Works]`  
  
 `where [Product].[Product Line].[Mountain]`  
  
 Produce el siguiente conjunto de resultados:  
  
|||||  
|-|-|-|-|  
||**Reseller Sales Amount**|**Discount Amount**|**PCT Discount**|  
|**Mountain-200**|**$14,356,699.36**|**$19,012.71**|**0,13 %**|  
|**Mountain-100**|**$8,568,958.27**|**$139,393.27**|**1,63 %**|  
|**HL Mountain Frame**|**$3,365,069.27**|**$174.11**|**0,01 %**|  
|**Mountain-300**|**$1,907,249.38**|**$876.95**|**0,05 %**|  
|**Mountain-500**|**$1,067,327.31**|**$17,266.09**|**1,62 %**|  
|**Mountain-400-W**|**$592,450.05**|**$303.49**|**0,05 %**|  
|**LL Mountain Frame**|**$521,864.42**|**$252.41**|**0,05 %**|  
|**ML Mountain Frame-W**|**$482,953.16**|**$206.95**|**0.04%**|  
|**ML Mountain Frame**|**$343,785.29**|**$161.82**|**0,05 %**|  
|**Women's Mountain Shorts**|**$260,304.09**|**$6,675.56**|**2,56 %**|  
  
 En el conjunto de resultados anterior, podemos observar siete nuevas entradas en la lista de Top10SellingProducts, y también podemos observar que Mountain-200, Mountain-100 y HL Mountain Frame se han movido a la parte superior de la lista. En el conjunto de resultados anterior, esos tres valores se intercalaban.  
  
 Esto es lo que se denomina Autoexists en modo profundo, porque el conjunto Top10SellingProducts se evalúa para cumplir las condiciones de segmentación de la consulta. El modo Deep Autoexists implica que todas las expresiones se evaluarán para cumplir el espacio más profundo posible después de aplicar las expresiones del segmentador, las expresiones de subselección del eje, etc.  
  
 No obstante, es posible que algún usuario desee poder realizar el análisis sobre Top10SellingProducts como equivalente de Preferred10Products, como en el siguiente ejemplo:  
  
 `with member [Measures].[PCT Discount] AS '[Measures].[Discount Amount]/[Measures].[Reseller Sales Amount]', FORMAT_STRING = 'Percent'`  
  
 `set Top10SellingProducts as 'topcount([Product].[Model Name].children, 10, [Measures].[Reseller Sales Amount])'`  
  
 `set Preferred10Products as '`  
  
 `{[Product].[Model Name].&[Mountain-200],`  
  
 `[Product].[Model Name].&[Road-250],`  
  
 `[Product].[Model Name].&[Mountain-100],`  
  
 `[Product].[Model Name].&[Road-650],`  
  
 `[Product].[Model Name].&[Touring-1000],`  
  
 `[Product].[Model Name].&[Road-550-W],`  
  
 `[Product].[Model Name].&[Road-350-W],`  
  
 `[Product].[Model Name].&[HL Mountain Frame],`  
  
 `[Product].[Model Name].&[Road-150],`  
  
 `[Product].[Model Name].&[Touring-3000]`  
  
 `}'`  
  
 `select {[Measures].[Reseller Sales Amount], [Measures].[Discount Amount], [Measures].[PCT Discount]} on 0,`  
  
 `Preferred10Products on 1`  
  
 `from [Adventure Works]`  
  
 `where [Product].[Product Line].[Mountain]`  
  
 Produce el siguiente conjunto de resultados:  
  
|||||  
|-|-|-|-|  
||**Reseller Sales Amount**|**Discount Amount**|**PCT Discount**|  
|**Mountain-200**|**$14,356,699.36**|**$19,012.71**|**0,13 %**|  
|**Mountain-100**|**$8,568,958.27**|**$139,393.27**|**1,63 %**|  
|**HL Mountain Frame**|**$3,365,069.27**|**$174.11**|**0,01 %**|  
  
 En los resultados anteriores, la segmentación arroja un resultado que solamente incluye los productos Preferred10Products que forman parte del grupo [Mountain] de [Product].[Product Line]; es el resultado esperado, porque Preferred10Products es una expresión constante.  
  
 Este conjunto de resultados también se entiende como modo superficial de Autoexists. Esto se debe a que la expresión se evalúa antes de la cláusula de segmentación. En el ejemplo anterior, la expresión era una expresión constante a efectos de explicación del concepto.  
  
 Es posible modificar el comportamiento de Autoexists en el nivel de sesión mediante la propiedad de cadena de conexión **Autoexists** . En el ejemplo siguiente, para empezar se abre una nueva sesión y se agrega la propiedad *Autoexists=3* a la cadena de conexión. Se debe abrir una nueva conexión para llevar a cabo el ejemplo. Una vez establecida la conexión con el valor de Autoexist, permanecerá en vigor hasta que finalice la conexión.  
  
 `with member [Measures].[PCT Discount] AS '[Measures].[Discount Amount]/[Measures].[Reseller Sales Amount]', FORMAT_STRING = 'Percent'`  
  
 `set Top10SellingProducts as 'topcount([Product].[Model Name].children, 10, [Measures].[Reseller Sales Amount])'`  
  
 `//Preferred10Products set removed for clarity`  
  
 `select {[Measures].[Reseller Sales Amount], [Measures].[Discount Amount], [Measures].[PCT Discount]} on 0,`  
  
 `Top10SellingProducts on 1`  
  
 `from [Adventure Works]`  
  
 `where [Product].[Product Line].[Mountain]`  
  
 El siguiente conjunto de resultados muestra el comportamiento superficial de Autoexists.  
  
|||||  
|-|-|-|-|  
||**Reseller Sales Amount**|**Discount Amount**|**PCT Discount**|  
|**Mountain-200**|**$14,356,699.36**|**$19,012.71**|**0,13 %**|  
|**Mountain-100**|**$8,568,958.27**|**$139,393.27**|**1,63 %**|  
|**HL Mountain Frame**|**$3,365,069.27**|**$174.11**|**0,01 %**|  
  
 Comportamiento de Autoexists puede modificarse mediante el AUTOEXISTS = [1 | 2 | 3] parámetro en la cadena de conexión; vea [admite propiedades XMLA &#40;XMLA&#41; ](../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md) y <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A> para el uso de parámetros.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se devuelve la suma de la `Measures.[Order Quantity]` miembro, que se agrega en los primeros ocho meses del año 2003 incluidos en el `Date` dimensión, desde el **Adventure Works** cubo.  
  
```  
WITH MEMBER [Date].[Calendar].[First8Months2003] AS  
    Aggregate(  
        PeriodsToDate(  
            [Date].[Calendar].[Calendar Year],   
            [Date].[Calendar].[Month].[August 2003]  
        )  
    )  
SELECT   
    [Date].[Calendar].[First8Months2003] ON COLUMNS,  
    [Product].[Category].Children ON ROWS  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Order Quantity]  
```  
  
 Para entender **NON VISUAL** en el ejemplo siguiente es una consulta de [Adventure Works] para obtener las cifras de [Reseller Sales Amount] en una tabla donde las categorías de producto son las columnas y los tipos comerciales de revendedor son las filas. Observe que los totales se proporcionan para productos y revendedores.  
  
 La instrucción SELECT siguiente:  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from [Adventure Works]`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 Produce los siguientes resultados:  
  
|||||||  
|-|-|-|-|-|-|  
||**All Products**|**Accessories**|**Bikes**|**Clothing**|**Components**|  
|**All Resellers**|**$80,450,596.98**|**$571,297.93**|**$66,302,381.56**|**$1,777,840.84**|**$11,799,076.66**|  
|**Specialty Bike Shop**|**$6,756,166.18**|**$65,125.48**|**$6,080,117.73**|**$252,933.91**|**$357,989.07**|  
|**Value Added Reseller**|**$34,967,517.33**|**$175,002.81**|**$30,892,354.33**|**$592,385.71**|**$3,307,774.48**|  
|**Warehouse**|**$38,726,913.48**|**$331,169.64**|**$29,329,909.50**|**$932,521.23**|**$8,133,313.11**|  
  
 Para generar una tabla con datos solo para los productos Accessories y Clothing, y los revendedores Value Added Reseller y Warehouse, manteniendo todavía los totales globales, se podría escribir de la forma siguiente utilizando NON VISUAL:  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from NON VISUAL (Select {[Category].Accessories, [Category].Clothing} on 0,`  
  
 `{[Business Type].[Value Added Reseller], [Business Type].[Warehouse]} on 1`  
  
 `from [Adventure Works])`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 Produce los siguientes resultados:  
  
|||||  
|-|-|-|-|  
||**All Products**|**Accessories**|**Clothing**|  
|**All Resellers**|**$80,450,596.98**|**$571,297.93**|**$1,777,840.84**|  
|**Value Added Reseller**|**$34,967,517.33**|**$175,002.81**|**$592,385.71**|  
|**Warehouse**|**$38,726,913.48**|**$331,169.64**|**$932,521.23**|  
  
 Para generar una tabla que sume visualmente las columnas pero que tome el total real de todos [Category] para los totales de las filas, debe emitirse la consulta siguiente:  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from NON VISUAL (Select {[Category].Accessories, [Category].Clothing} on 0`  
  
 `from ( Select {[Business Type].[Value Added Reseller], [Business Type].[Warehouse]} on 0`  
  
 `from [Adventure Works])`  
  
 `)`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 Observe cómo NON VISUAL se aplica solamente a [Category].  
  
 La consulta anterior genera los resultados siguientes:  
  
|||||  
|-|-|-|-|  
||All Products|Accessories|Clothing|  
|All Resellers|$73,694,430.80|$506,172.45|$1,524,906.93|  
|Value Added Reseller|$34,967,517.33|$175,002.81|$592,385.71|  
|Warehouse|$38,726,913.48|$331,169.64|$932,521.23|  
  
 Al comparar con los resultados anteriores, puede observar que la fila [All Resellers] suma ahora hasta los valores mostrados para [Value Added Reseller] y [Warehouse], pero que la columna [All Products] muestra el valor total de todos los productos, incluso los que no se muestran.  
  
 En el ejemplo siguiente se demuestra cómo utilizar miembros calculados en subselecciones para filtrar en ellas. Para poder reproducir este ejemplo, se debe establecer la conexión con el parámetro de cadena de conexión *subconsultas = 1*.  
  
 `select Measures.allmembers on 0`  
  
 `from (`  
  
 `Select { [Measures].[Reseller Sales Amount]`  
  
 `, [Measures].[Reseller Total Product Cost]`  
  
 `, [Measures].[Reseller Gross Profit]`  
  
 `, [Measures].[Reseller Gross Profit Margin]`  
  
 `} on 0`  
  
 `from [Adventure Works]`  
  
 `)`  
  
 La consulta anterior genera los resultados siguientes:  
  
|||||  
|-|-|-|-|  
|Reseller Sales Amount|Reseller Total Product Cost|Reseller Gross Profit|Reseller Gross Profit Margin|  
|$80,450,596.98|$79,980,114.38|$470,482.60|0.58%|  
  
## <a name="see-also"></a>Vea también  
 [Conceptos clave para MDX &#40;Analysis Services&#41;](../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)   
 [Instrucciones de manipulación de datos MDX &#40;MDX&#41;](../mdx/mdx-data-manipulation-statements-mdx.md)   
 [Restringir la consulta con ejes de consulta y segmentador &#40;MDX&#41;](~/analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-restricting-the-query.md)  
  
  

