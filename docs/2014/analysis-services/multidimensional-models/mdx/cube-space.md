---
title: Espacio de cubo | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: c3a012b4-9ca0-4fb8-9c26-5ecc0e2e2b2b
caps.latest.revision: 6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d0bcd66844f5eaacca291cd67e84e34b6222788c
ms.sourcegitcommit: 01fccb8015644e75fd99fc5543d8216a1539f6ca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/10/2018
ms.locfileid: "40392124"
---
# <a name="cube-space"></a>Espacio de cubo
  El espacio de cubo es el producto de los miembros de las jerarquías de atributo de un cubo con las medidas de un cubo. Por consiguiente, el espacio del cubo se determina con el producto combinatorio de todos los miembros de jerarquía de atributo en el cubo y las medidas del cubo, y define el tamaño máximo del cubo. Es importante tener en cuenta que este espacio incluye todas las posibles combinaciones de miembros de la jerarquía de atributos, incluso las que podrían ser consideradas como imposibles en el mundo real, es decir, aquellas en las que la ciudad es París y los países son Gran Bretaña, España, Japón, India, etc.  
  
## <a name="autoexists-and-cube-space"></a>Espacio de cubo y Autoexist  
 El concepto de *autoexist* limita este espacio de cubo a aquellas celdas que realmente existen. Los miembros de una jerarquía de atributo de una dimensión pueden no existir con los miembros de otra jerarquía de atributo de la misma dimensión.  
  
 Por ejemplo, si tiene un cubo con una jerarquía de atributo City, una jerarquía de atributo Country y una medida Internet Sales Amount, el espacio de este cubo solamente incluye a los miembros que existen entre sí. Por ejemplo, si la jerarquía de atributo City incluye las ciudades de Nueva York, Londres, París, Tokio y Melbourne; y la jerarquía de atributo Country incluye los países Estados Unidos, Reino Unido, Francia, Japón y Australia; entonces el espacio del cubo no incluye el espacio (celda) en la intersección de París y Estados Unidos.  
  
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
  
 La consulta anterior solo devuelve celdas para los miembros de cada jerarquía de atributo de la consulta que existen entre sí. También se puede escribir la consulta anterior con el nuevo * variant de la [ \* (Crossjoin) (MDX)](/sql/mdx/crossjoin-mdx) función.  
  
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
  
 Cada una de estas tres consultas anteriores muestra el efecto del comportamiento de auto-exists en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="user-defined-hierarchies-and-cube-space"></a>Jerarquías definidas por el usuario y espacio de cubo  
 Los ejemplos anteriores de este tema definen posiciones en el espacio de cubo mediante jerarquías de atributo. Sin embargo, también se puede definir una posición en un espacio de cubo mediante jerarquías definidas por el usuario que se han definido en base a las jerarquías de atributo de una dimensión. Una jerarquía definida por el usuario es una jerarquía de jerarquías de atributo diseñadas para facilitar la exploración del cubo por parte de los usuarios.  
  
 Por ejemplo, la consulta `CROSSJOIN` de la sección anterior también pudo haber sido escrita de la siguiente manera:  
  
```  
SELECT CROSSJOIN  
   (  
      {[Customer].[Country].[United States]},  
         [Customer].[Customer Geography].[State-Province].Members  
   )   
ON 0   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
 En la consulta anterior, la jerarquía definida por el usuario Customer Geography de la dimensión Customer se utiliza para definir la posición en el espacio de cubo que se definió anteriormente mediante una jerarquía de atributo. La posición idéntica en el espacio de cubo puede definirse mediante jerarquías de atributo o jerarquías definidas por el usuario.  
  
##  <a name="AttribRelationships"></a> Relaciones de atributo y espacio de cubo  
 El definir relaciones de atributo entre atributos relacionados mejora el rendimiento de las consultas (al facilitar la creación de agregaciones apropiadas) y afecta al miembro de una jerarquía de atributo relacionada que aparece con un miembro de jerarquía de atributo. Por ejemplo, cuando define una tupla que incluye a un miembro de la jerarquía de atributo City y la tupla no define explícitamente al miembro de la jerarquía de atributo Country, se puede esperar que el miembro de la jerarquía de atributo predeterminada Country sea el miembro relacionado de la jerarquía de atributo Country. Sin embargo, esto es cierto solo si se define una relación de atributo entre la jerarquía de atributo City y la jerarquía de atributo Country.  
  
 El ejemplo siguiente devuelve el miembro de una jerarquía de atributo relacionada que no está incluida explícitamente en la consulta.  
  
```  
WITH MEMBER Measures.x AS   
   Customer.Country.CurrentMember.Name  
SELECT Measures.x ON 0,  
Customer.City.Members ON 1  
FROM [Adventure Works]  
```  
  
> [!NOTE]  
>  Tenga en cuenta que el `WITH` palabra clave se usa con el [CurrentMember (MDX)](/sql/mdx/current-mdx) y [Name (MDX)](/sql/mdx/members-string-mdx) funciones para crear un miembro calculado para su uso en la consulta. Para más información, vea [Consulta de MDX básica &#40;MDX&#41;](mdx-query-the-basic-query.md).  
  
 En la consulta anterior, se devuelve el nombre del miembro de la jerarquía de atributo Country asociado con cada miembro de la jerarquía de atributo State. Aparece el miembro Country esperado (debido a que hay una relación de atributo definida entre los atributos City y Country). Sin embargo, si no se define una relación de atributo entre las jerarquías de atributo de la misma dimensión, se devuelve el miembro (All), como se muestra en la consulta siguiente.  
  
```  
WITH MEMBER Measures.x AS   
   Customer.Education.Currentmember.Name  
SELECT Measures.x  ON 0,   
Customer.City.Members ON 1  
FROM [Adventure Works]  
```  
  
 En la consulta anterior, se devuelve el miembro (All) ("All Customers"), debido a que no hay una relación entre Education y City. Por lo tanto, el miembro (All) de la jerarquía de atributo Education sería el miembro predeterminado de la jerarquía de atributo Education utilizada en cualquier tupla en la que interviniera la jerarquía de atributo City y no se proporcionara explícitamente un miembro Education.  
  
## <a name="calculation-context"></a>Contexto de cálculo  
  
## <a name="see-also"></a>Vea también  
 [Conceptos clave para MDX &#40;Analysis Services&#41;](../key-concepts-in-mdx-analysis-services.md)   
 [Tuplas](tuples.md)   
 [Autoexists](autoexists.md)   
 [Trabajar con miembros, tuplas y conjuntos &#40;MDX&#41;](working-with-members-tuples-and-sets-mdx.md)   
 [Totales visuales y totales no visuales](visual-totals-and-non-visual-totals.md)   
 [Referencia del lenguaje MDX &#40;MDX&#41;](/sql/mdx/mdx-language-reference-mdx)   
 [Expresiones multidimensionales &#40;MDX&#41; referencia](/sql/mdx/multidimensional-expressions-mdx-reference)  
  
  
