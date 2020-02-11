---
title: DrilldownLevel (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b9c623a1e99053e796609dc82f27519f27c07a9d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68049293"
---
# <a name="drilldownlevel-mdx"></a>DrilldownLevel (MDX)


  Aumenta los detalles de los miembros de un conjunto a un nivel por debajo del nivel más bajo representado en el conjunto.  
  
 Especificar el nivel en el que explorar en profundidad es opcional, pero si establece el nivel, puede usar una **expresión de nivel** o el **nivel de índice**. Estos argumentos son mutuamente exclusivos. Por último, si los miembros calculados están presentes en la consulta, puede especificar un argumento para incluirlos en el conjunto de filas.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
DrilldownLevel(Set_Expression [,[Level_Expression] ,[Index]] [,INCLUDE_CALC_MEMBERS])  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Level_Expression*  
 (Opcional). Expresión MDX que identifica de forma explícita el nivel en el que aumentar los detalles. Si especifica una expresión de nivel, omita el siguiente argumento de índice.  
  
 *Ajustar*  
 (Opcional). Expresión numérica válida que especifica el número de jerarquía para aumentar el nivel de detalle dentro del conjunto. Se puede usar el nivel del índice en lugar de Level_Expression para identificar de forma explícita el nivel en el que aumentar los detalles.  
  
 *Include_Calc_Members*  
 (Opcional). Marca que indica si se deben incluir en el nivel de detalle los miembros calculados, si existen.  
  
## <a name="remarks"></a>Observaciones  
 La función **DrilldownLevel** devuelve un conjunto de miembros secundarios en un orden jerárquico, basado en los miembros incluidos en el conjunto especificado. El orden se mantiene entre los miembros originales del conjunto especificado, aunque todos los miembros secundarios incluidos en el conjunto de resultados de la función se incluyen inmediatamente bajo su miembro primario.  
  
 Si hay una estructura de datos jerárquica de varios niveles, puede elegir de forma explícita un nivel en el que aumentar los detalles. Hay dos métodos, que se excluyen mutuamente, de especificar el nivel. El primer enfoque consiste en establecer el argumento **Level_Expression** mediante una expresión MDX que devuelve el nivel, un enfoque alternativo consiste en especificar el argumento de **Índice** mediante una expresión numérica que especifica el nivel por número.  
  
 Si se especifica una expresión de nivel, la función crea un conjunto en un orden jerárquico mediante la recuperación de los elementos secundarios de solo aquellos miembros que se encuentran en el nivel especificado. Si se especifica una expresión de nivel y no hay ningún miembro en ese nivel, la expresión de nivel no se tiene en cuenta.  
  
 Si se especifica un valor del índice, la función crea un conjunto en orden jerárquico mediante la recuperación de los elementos secundarios de solo aquellos miembros que se encuentran en el nivel más bajo siguiente de la jerarquía a la que se hace referencia en el conjunto especificado, en función de un índice basado en cero dado.  
  
 Si no se especifica una expresión de nivel ni un valor de índice, la función crea un conjunto en orden jerárquico mediante la recuperación de los elementos secundarios de solo aquellos miembros que se encuentran en el nivel más bajo de la primera dimensión a la que se hace referencia en el conjunto especificado.  
  
 La consulta de la propiedad XMLA MdpropMdxDrillFunctions permite comprobar el nivel de compatibilidad que el servidor proporciona para las funciones de perforación. para más información, consulte [las propiedades XMLA compatibles &#40;&#41;XMLA](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) .  
  
## <a name="examples"></a>Ejemplos  
 Puede probar los ejemplos siguientes en la ventana de consulta MDX de SSMS, utilizando el cubo de Adventure Works.  
  
 **Ejemplo 1: muestra la sintaxis mínima**  
  
 En el primer ejemplo se muestra la sintaxis mínima de **DrilldownLevel**. El único argumento necesario es una expresión de conjunto. Tenga en cuenta que al ejecutar esta consulta, obtiene el elemento primario [todas las categorías] y los miembros del siguiente nivel inferior: [accessories], [Bikes], etc. Aunque este ejemplo es sencillo, muestra el propósito básico de la función **DrilldownLevel** , que está profundizando hasta el siguiente nivel que aparece a continuación.  
  
```  
SELECT DRILLDOWNLEVEL({[Product].[Product Categories]} * {[Sales Territory].[Sales Territory]}}) ON COLUMNS  
FROM [Adventure Works]  
```  
  
 Ejemplo 2: sintaxis alternativa con un nivel de índice explícito  
  
 En este ejemplo se muestra la sintaxis alternativa, en la que se especifica un nivel del índice mediante una expresión numérica. En este caso, el nivel del índice es 0. En el caso de un índice basado en cero, es el nivel más bajo.  
  
```  
SELECT  
DRILLDOWNLEVEL({[Product].[Product Categories]} * {[Sales Territory].[Sales Territory]},,0) ON COLUMNS  
FROM [Adventure Works]  
```  
  
 Observe que el conjunto de resultados es idéntico al de la consulta anterior. Por regla general, no es necesario establecer el nivel del índice a menos que se desee que los detalles empiecen en un nivel concreto. Vuelva a ejecutar la consulta anterior, estableciendo el valor del índice en 1 y, después, en 2. Con el valor del índice establecido en 1, los detalles empiezan en el segundo nivel de la jerarquía. Con el valor del índice establecido en 2, los detalles empiezan en el tercer nivel, que es el nivel más alto en este ejemplo. Cuanto más alta es la expresión numérica, más alto es el nivel del índice.  
  
 **Ejemplo 3: muestra una expresión de nivel**  
  
 En el ejemplo siguiente se muestra cómo usar una expresión de nivel. Con un conjunto dado que represente una estructura jerárquica, el uso de una expresión de nivel le permite elegir un nivel de la jerarquía para empezar el aumento de los detalles.  
  
 En este ejemplo, el nivel de exploración en profundidad comienza en [City], como el segundo argumento de la función **DrilldownLevel** . Al ejecutar esta consulta, el aumento de detalles empieza en el nivel [City], para los estados de Washington y Oregón. Según la función **DrilldownLevel** , el conjunto de resultados también incluye miembros en el siguiente nivel inferior, [postal Codes].  
  
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
  
 **Ejemplo 4: incluir miembros calculados**  
  
 En el último ejemplo se muestra un miembro calculado, que aparece en la parte inferior del conjunto de resultados al agregar la marca de **include_calculated_members** . Observe que la marca se especifica como cuarto parámetro.  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
