---
title: Autoexists | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 56283497-624c-45b5-8a0d-036b0e331d22
author: minewiskan
ms.author: owend
ms.openlocfilehash: dd35958a364456c12d58392afe3754f6adcf97b8
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2020
ms.locfileid: "84546597"
---
# <a name="autoexists"></a>autoexist
  El concepto de *autoexists* limita el espacio del cubo a esas celdas que realmente existen en el cubo en contraposición a aquellas que podrían existir como resultado de la creación de todas las posibles combinaciones de miembros de jerarquía de atributo a partir de la misma jerarquía. Esto es así porque los miembros de una jerarquía de atributo no pueden existir con los miembros de otra jerarquía de atributo de la misma dimensión. Cuando dos o más jerarquías de atributos de la dimensión se usan en una instrucción SELECT, Analysis Services evalúa las expresiones de los atributos para asegurarse de que los miembros de dichos atributos están correctamente delimitados, a fin de cumplir los criterios de todos los demás atributos.  
  
 Por ejemplo, supongamos que está trabajando con atributos de la dimensión Geography. Si tiene una expresión que devuelve todos los miembros del atributo City, y otra expresión que delimita los miembros del atributo Country a todos los países de Europa, los miembros de City quedarán delimitados a aquellas ciudades que pertenezcan únicamente a países de Europa. Esto es debido a la característica de autoexists de Analysis Services. Autoexists solamente se aplica a atributos de una misma dimensión porque intenta impedir que los registros de la dimensión excluidos de una expresión de atributos se incluyan en las demás expresiones de atributos. Autoexists también puede entenderse como la intersección resultante de las distintas expresiones de atributos de las filas de la dimensión.  
  
## <a name="cell-existence"></a>Existencia de celdas  
 Las siguientes celdas siempre existen:  
  
-   El miembro (All), de cada jerarquía, cuando se cruza con miembros de otras jerarquías de la misma dimensión.  
  
-   Los miembros calculados cuando se cruzan con los elementos del mismo nivel no calculados o con los miembros primarios o descendientes de los elementos del mismo nivel no calculados.  
  
## <a name="providing-non-existing-cells"></a>Proporcionar celdas no existentes  
 Una celda no existente es una celda proporcionada por el sistema como respuesta a una consulta o cálculo que solicita una celda que no existe en el cubo. Por ejemplo, si tiene un cubo con una jerarquía de atributo City y una jerarquía de atributo Country que pertenece a la dimensión Geography, y la medida Internet Sales Amount, el espacio de este cubo solamente incluye a los miembros que existen entre sí. Por ejemplo, si la jerarquía de atributo City incluye las ciudades de Nueva York, Londres, París, Tokio y Melbourne; y la jerarquía de atributo Country incluye los países Estados Unidos, Reino Unido, Francia, Japón y Australia; entonces el espacio del cubo no incluye el espacio (celda) en la intersección de París y Estados Unidos.  
  
 Al consultar las celdas que no existen, las celdas no existentes devuelven valores nulos; es decir, no pueden contener cálculos y no se puede definir un cálculo que escriba en este espacio. Por ejemplo, la siguiente instrucción incluye celdas que no existen.  
  
```  
SELECT [Customer].[Gender].[Gender].Members ON COLUMNS,  
{[Customer].[Customer].[Aaron A. Allen]  
   ,[Customer].[Customer].[Abigail Clark]} ON ROWS   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
> [!NOTE]  
>  Esta consulta usa la función [Members (Set) (MDX)](/sql/mdx/members-set-mdx) para devolver el conjunto de miembros de la jerarquía de atributo Gender en el eje de columnas y cruza este conjunto con el conjunto especificado de miembros de la jerarquía de atributo Customer en el eje de filas.  
  
 Cuando se ejecuta la consulta anterior, la celda en la intersección de Aaron A. Allen y Female muestra un valor nulo. De igual manera, la celda en la intersección de Abigail Clark y Male muestra un valor nulo. Estas celdas no existen y no pueden contener un valor, pero las celdas que no existen pueden aparecer en el resultado devuelto por una consulta.  
  
 Al usar la función [Crossjoin (MDX)](/sql/mdx/crossjoin-mdx) para devolver el producto cruzado de los miembros de la jerarquía de atributo de las jerarquías de atributo de la misma dimensión, auto-exists limita las tuplas devueltas al conjunto de tuplas que realmente existen, en lugar de devolver un producto cartesiano completo. Por ejemplo, ejecute y examine los resultados de la ejecución de la siguiente consulta.  
  
```  
SELECT CROSSJOIN  
   (  
      {[Customer].[Country].[United States]},  
         [Customer].[State-Province].Members  
  ) ON 0   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
> [!NOTE]  
>  Observe que 0 se utiliza para designar al eje de columna, que es una abreviatura para el eje(0), que es el eje de columna.  
  
 La consulta anterior solo devuelve celdas para los miembros de cada jerarquía de atributo de la consulta que existen entre sí. La consulta anterior también puede escribirse con la nueva variante * de la función [Crossjoin (MDX)](/sql/mdx/crossjoin-mdx) .  
  
```  
SELECT   
   [Customer].[Country].[United States] *   
      [Customer].[State-Province].Members  
ON 0   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
 La consulta anterior también se podría escribir de la siguiente manera:  
  
```  
SELECT [Customer].[State-Province].Members  
ON 0   
FROM [Adventure Works]  
WHERE (Measures.[Internet Sales Amount],  
   [Customer].[Country].[United States])  
```  
  
 Los valores de celda devueltos serán idénticos, aunque los metadatos del conjunto de resultados serán diferentes. Por ejemplo, con la consulta anterior, la jerarquía Country se movió al eje segmentador (en la cláusula WHERE), por lo que no aparece explícitamente en el conjunto de resultados.  
  
 Cada una de estas tres consultas anteriores muestra el efecto del comportamiento de autoexists en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] .  
  
## <a name="deep-and-shallow-autoexists"></a>Deep y Shallow Autoexists  
 Autoexists se puede aplicar a las expresiones como Deep y Shallow. `Deep Autoexists` quiere decir que todas las expresiones se evaluarán para cumplir el espacio más profundo posible después de aplicar las expresiones de eje segmentador, expresiones de subselección en el eje, etc. `Shallow Autoexists` quiere decir que las expresiones externas se evalúan antes que la expresión actual y los resultados se pasan a la expresión actual. El valor predeterminado es deep autoexists.  
  
 El siguiente escenario y ejemplos ayudarán a mostrar los tipos diferentes de autoexists. En los ejemplos siguientes, se crearán dos conjuntos: uno de ellos como una expresión calculada, y el otro como una expresión constante.  
  
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
|**Mountain-200**|**$14,356,699.36**|**$19,012.71**|**0,13%**|  
|**Road-250**|**$9,377,457.68**|**$4,032.47**|**0,04 %**|  
|**Mountain-100**|**$8,568,958.27**|**$139,393.27**|**1,63%**|  
|**Road-650**|**$7,442,141.81**|**$39,698.30**|**0,53 %**|  
|**Touring-1000**|**$6,723,794.29**|**$166,144.17**|**2,47%**|  
|**Road-550-W**|**$3,668,383.88**|**$1,901.97**|**0,05%**|  
|**Road-350-W**|**$3,665,932.31**|**$20,946.50**|**0,57%**|  
|**HL Mountain Frame**|**$3,365,069.27**|**$174.11**|**0,01%**|  
|**Road-150**|**$2,363,805.16**|**$0,00**|**0.00%**|  
|**Touring-3000**|**$2,046,508.26**|**$79,582.15**|**3,89%**|  
  
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
|**Mountain-200**|**$14,356,699.36**|**$19,012.71**|**0,13%**|  
|**Road-250**|**$9,377,457.68**|**$4,032.47**|**0,04 %**|  
|**Mountain-100**|**$8,568,958.27**|**$139,393.27**|**1,63%**|  
|**Road-650**|**$7,442,141.81**|**$39,698.30**|**0,53 %**|  
|**Touring-1000**|**$6,723,794.29**|**$166,144.17**|**2,47%**|  
|**Road-550-W**|**$3,668,383.88**|**$1,901.97**|**0,05%**|  
|**Road-350-W**|**$3,665,932.31**|**$20,946.50**|**0,57%**|  
|**HL Mountain Frame**|**$3,365,069.27**|**$174.11**|**0,01%**|  
|**Road-150**|**$2,363,805.16**|**$0,00**|**0.00%**|  
|**Touring-3000**|**$2,046,508.26**|**$79,582.15**|**3,89%**|  
  
 En el siguiente ejemplo se ilustrará el concepto de Autoexists en modo profundo. En el ejemplo, Top10SellingProducts se filtra por el atributo [Product].[Product Line] para los productos del grupo [Mountain]. Tenga en cuenta que ambos atributos (slicer y axis) pertenecen a la misma dimensión, [Product].  
  
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
|**Mountain-200**|**$14,356,699.36**|**$19,012.71**|**0,13%**|  
|**Mountain-100**|**$8,568,958.27**|**$139,393.27**|**1,63%**|  
|**HL Mountain Frame**|**$3,365,069.27**|**$174.11**|**0,01%**|  
|**Mountain-300**|**$1,907,249.38**|**$876.95**|**0,05%**|  
|**Mountain-500**|**$1,067,327.31**|**$17,266.09**|**1,62%**|  
|**Mountain-400-W**|**$592,450.05**|**$303.49**|**0,05%**|  
|**LL Mountain Frame**|**$521,864.42**|**$252.41**|**0,05%**|  
|**ML Mountain Frame-W**|**$482,953.16**|**$206,95**|**0,04 %**|  
|**ML Mountain Frame**|**$343,785.29**|**$161.82**|**0,05%**|  
|**Women's Mountain Shorts**|**$260,304.09**|**$6,675.56**|**2,56%**|  
  
 En el conjunto de resultados anterior se muestran siete nuevas entradas en la lista Top10SellingProducts y, además, vemos que Mountain-200, Mountain-100 y HL Mountain Frame se han movido a la parte superior de la lista. En el conjunto de resultados anterior, esos tres valores se intercalaban.  
  
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
|**Mountain-200**|**$14,356,699.36**|**$19,012.71**|**0,13%**|  
|**Mountain-100**|**$8,568,958.27**|**$139,393.27**|**1,63%**|  
|**HL Mountain Frame**|**$3,365,069.27**|**$174.11**|**0,01%**|  
  
 En los resultados anteriores, la segmentación arroja un resultado que solamente incluye los productos Preferred10Products que forman parte del grupo [Mountain] de [Product].[Product Line]; es el resultado esperado, porque Preferred10Products es una expresión constante.  
  
 Este conjunto de resultados también se entiende como shallow autoexists. Esto se debe a que la expresión se evalúa antes de la cláusula de segmentación. En el ejemplo anterior, la expresión era una expresión constante a efectos de explicación del concepto.  
  
 Es posible modificar el comportamiento de Autoexists en el nivel de sesión mediante la propiedad de cadena de conexión `Autoexists`. En el ejemplo siguiente, para empezar se abre una nueva sesión y se agrega la propiedad *Autoexists=3* a la cadena de conexión. Se debe abrir una nueva conexión para llevar a cabo el ejemplo. Una vez establecida la conexión con el valor de Autoexist, permanecerá en vigor hasta que finalice la conexión.  
  
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
|**Mountain-200**|**$14,356,699.36**|**$19,012.71**|**0,13%**|  
|**Mountain-100**|**$8,568,958.27**|**$139,393.27**|**1,63%**|  
|**HL Mountain Frame**|**$3,365,069.27**|**$174.11**|**0,01%**|  
  
 El comportamiento de autoexists se puede modificar mediante el parámetro autoexists = [1 | 2 | 3] en la cadena de conexión; vea [las propiedades XMLA admitidas &#40;xmla&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) y <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A> para el uso de parámetros.  
  
## <a name="see-also"></a>Consulte también  
 [Conceptos clave de &#40;MDX Analysis Services&#41;](../key-concepts-in-mdx-analysis-services.md)   
 [Espacio de cubo](cube-space.md)   
 [Tuplas](tuples.md)   
 [Trabajar con miembros, tuplas y conjuntos &#40;&#41;MDX](working-with-members-tuples-and-sets-mdx.md)   
 [Totales visuales y totales no visuales](visual-totals-and-non-visual-totals.md)   
 [Referencia del lenguaje MDX &#40;MDX&#41;](/sql/mdx/mdx-language-reference-mdx)   
 [Referencia de expresiones multidimensionales &#40;MDX&#41;](/sql/mdx/multidimensional-expressions-mdx-reference)  
  
  
