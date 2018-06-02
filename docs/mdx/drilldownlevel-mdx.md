---
title: DrilldownLevel (MDX) | Documentos de Microsoft
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 99e8c47164d920ec531bf6ab51e35979b060c35d
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34578007"
---
# <a name="drilldownlevel-mdx"></a>DrilldownLevel (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Aumenta los detalles de los miembros de un conjunto a un nivel por debajo del nivel más bajo representado en el conjunto.  
  
 Especifican el nivel en el que se va a explorar hacia abajo es opcional, pero si establece el nivel, puede utilizar cualquiera una **nivel expresión** o **nivel de índice**. Estos argumentos son mutuamente exclusivos. Por último, si los miembros calculados están presentes en la consulta, puede especificar un argumento para incluirlos en el conjunto de filas.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
DrilldownLevel(Set_Expression [,[Level_Expression] ,[Index]] [,INCLUDE_CALC_MEMBERS])  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Level_Expression*  
 (Opcional). Expresión MDX que identifica de forma explícita el nivel en el que aumentar los detalles. Si especifica una expresión de nivel, omita el siguiente argumento de índice.  
  
 *Index*  
 (Opcional). Expresión numérica válida que especifica el número de jerarquía para aumentar el nivel de detalle dentro del conjunto. Se puede usar el nivel del índice en lugar de Level_Expression para identificar de forma explícita el nivel en el que aumentar los detalles.  
  
 *Include_Calc_Members*  
 (Opcional). Marca que indica si se deben incluir en el nivel de detalle los miembros calculados, si existen.  
  
## <a name="remarks"></a>Notas  
 El **DrilldownLevel** función devuelve un conjunto de secundarios miembros en un orden jerárquico, basado en los miembros incluidos en el conjunto especificado. El orden se mantiene entre los miembros originales del conjunto especificado, aunque todos los miembros secundarios incluidos en el conjunto de resultados de la función se incluyen inmediatamente bajo su miembro primario.  
  
 Si hay una estructura de datos jerárquica de varios niveles, puede elegir de forma explícita un nivel en el que aumentar los detalles. Hay dos métodos, que se excluyen mutuamente, de especificar el nivel. El primer enfoque consiste en establecer el **level_expression** argumento utilizando una expresión MDX que devuelve el nivel, una solución alternativa consiste en especificar el **índice** argumento, utilizando una expresión numérica que especifica el nivel por número.  
  
 Si se especifica una expresión de nivel, la función crea un conjunto en un orden jerárquico mediante la recuperación de los elementos secundarios de solo aquellos miembros que se encuentran en el nivel especificado. Si se especifica una expresión de nivel y no hay ningún miembro en ese nivel, la expresión de nivel no se tiene en cuenta.  
  
 Si se especifica un valor del índice, la función crea un conjunto en orden jerárquico mediante la recuperación de los elementos secundarios de solo aquellos miembros que se encuentran en el nivel más bajo siguiente de la jerarquía a la que se hace referencia en el conjunto especificado, en función de un índice basado en cero dado.  
  
 Si se especifica una expresión de nivel ni un valor de índice, la función crea un conjunto en un orden jerárquico mediante la recuperación de los elementos secundarios de solo aquellos miembros que se encuentran en el nivel más bajo de la primera dimensión hace referencia en el conjunto especificado.  
  
 Consultar la propiedad XMLA MdpropMdxDrillFunctions le permite comprobar el nivel de compatibilidad que proporciona el servidor para las funciones obtener detalles. vea [admite propiedades XMLA &#40;XMLA&#41; ](../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md) para obtener más información.  
  
## <a name="examples"></a>Ejemplos  
 Puede probar los ejemplos siguientes en la ventana de consulta MDX de SSMS, utilizando el cubo de Adventure Works.  
  
 **Ejemplo 1: muestra la sintaxis mínima**  
  
 El primer ejemplo muestra la sintaxis mínima de **DrilldownLevel**. El único argumento necesario es una expresión de conjunto. Tenga en cuenta que al ejecutar esta consulta, obtendrá el primario [All Categories] y los miembros del siguiente nivel hacia abajo: [Accessories], [Bikes], y así sucesivamente. Aunque este ejemplo es sencillo, muestra la finalidad básica de la **DrilldownLevel** función, que es profundizando hasta el siguiente nivel inferior.  
  
```  
SELECT DRILLDOWNLEVEL({[Product].[Product Categories]} * {[Sales Territory].[Sales Territory]}}) ON COLUMNS  
FROM [Adventure Works]  
```  
  
 Ejemplo 2: sintaxis alternativa en la que se utiliza un nivel del índice explícito  
  
 En este ejemplo se muestra la sintaxis alternativa, en la que se especifica un nivel del índice mediante una expresión numérica. En este caso, el nivel del índice es 0. En el caso de un índice basado en cero, es el nivel más bajo.  
  
```  
SELECT  
DRILLDOWNLEVEL({[Product].[Product Categories]} * {[Sales Territory].[Sales Territory]},,0) ON COLUMNS  
FROM [Adventure Works]  
```  
  
 Observe que el conjunto de resultados es idéntico al de la consulta anterior. Por regla general, no es necesario establecer el nivel del índice a menos que se desee que los detalles empiecen en un nivel concreto. Vuelva a ejecutar la consulta anterior, estableciendo el valor del índice en 1 y, después, en 2. Con el valor del índice establecido en 1, los detalles empiezan en el segundo nivel de la jerarquía. Con el valor del índice establecido en 2, los detalles empiezan en el tercer nivel, que es el nivel más alto en este ejemplo. Cuanto más alta es la expresión numérica, más alto es el nivel del índice.  
  
 **Ejemplo 3: muestra una expresión de nivel**  
  
 En el ejemplo siguiente se muestra cómo usar una expresión de nivel. Con un conjunto dado que represente una estructura jerárquica, el uso de una expresión de nivel le permite elegir un nivel de la jerarquía para empezar el aumento de los detalles.  
  
 En este ejemplo, el nivel de detalle empieza en [City], como el segundo argumento de la **DrilldownLevel** función. Al ejecutar esta consulta, el aumento de detalles empieza en el nivel [City], para los estados de Washington y Oregón. Por el **DrilldownLevel** función, el resultado conjunto también incluye los miembros del siguiente nivel hacia abajo, [Postal codes].  
  
```  
SELECT [Measures].[Internet Sales Amount] ON COLUMNS,  
   NON EMPTY (  
   DRILLDOWNLEVEL(  
       {[Customer].[Customer Geography].[Country].[United States],  
           DESCENDANTS(  
             { [Customer].[Customer Geography].[State-Province].[Washington],    
               [Customer].[Customer Geography].[State-Province].[Oregon]},   
               [Customer].[Customer Geography].[City]) } ,  
[Customer].[Customer Geography].[City] ) )  ON ROWS  
FROM [Adventure Works]  
```  
  
 **Ejemplo 4: incluidos a los miembros calculados**  
  
 El último ejemplo se muestra un miembro calculado, que aparece en la parte inferior del resultado se establece al agregar el **include_calculated_members** marca. Observe que la marca se especifica como cuarto parámetro.  
  
 Este ejemplo funciona porque el miembro calculado está en el mismo nivel que los miembros no calculados. El miembro calculado [West Coast] está formado por miembros de [United States] más todos los miembros que están un nivel por debajo de [United States].  
  
```  
WITH MEMBER   
[Customer].[Customer Geography].[Country].&[United States].[West Coast] AS  
[Customer].[Customer Geography].[State-Province].&[OR]&[US] +  
[Customer].[Customer Geography].[State-Province].&[WA]&[US] +  
[Customer].[Customer Geography].[State-Province].&[CA]&[US]  
SELECT [Measures].[Internet Order Count] ON 0,  
DRILLDOWNLEVEL([Customer].[Customer Geography].[Country].&[United States],,,INCLUDE_CALC_MEMBERS) on 1  
FROM [Adventure Works]  
```  
  
 Si se quita la marca y se vuelva a ejecutar la consulta, se obtienen los mismos resultados, menos el miembro calculado, [West Coast].  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
