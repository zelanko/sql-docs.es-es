---
title: Existe (MDX) | Documentos de Microsoft
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 98f07985b83ae32f02bd3da68d382c8f3fceb0cf
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34578257"
---
# <a name="exists-mdx"></a>Exists (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve el conjunto de tuplas del primer conjunto especificado que existe con una o más tuplas del segundo conjunto especificado. Esta función realiza manualmente lo que Autoexist realiza automáticamente. Para obtener más información acerca de Autoexist existe, consulte [conceptos clave de MDX &#40;Analysis Services&#41;](../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md).  
  
 Si la parte opcional \<nombre del grupo de medida > es proporcionado, la función devuelve tuplas que existen con una o más tuplas del segundo conjunto y las tuplas que tienen filas asociadas en la tabla de hechos del grupo de medida especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Exists( Set_Expression1 , Set_Expression2 [, MeasureGroupName] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression1*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Set_Expression2*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *MeasureGroupName*  
 Expresión de cadena válida que especifica un nombre de grupo de medida.  
  
## <a name="remarks"></a>Notas  
  
1.  Filas de grupo de medida con medidas que contienen valores null contribuyen a **Exists** cuando se especifica el argumento MeasureGroupName. Esta es la diferencia entre esta forma de Exists y la función Nonempty: si la propiedad NullProcessing de estas medidas se establece en Preserve, significa que las medidas mostrarán valores Null cuando las consultas se ejecuten con esa parte del cubo; NonEmpty siempre quitará las tuplas de un conjunto que tenga valores de medidas Null, mientras que Exists con el argumento MeasureGroupName no filtrará las tuplas que tengan asociadas filas del grupo de medida, aun cuando los valores de medida sean Null.  
  
2.  Si *MeasureGroupName* se usa el parámetro, resultados dependerá de si hay medidas visibles en el grupo de medida que se hace referencia; si no hay ninguna acción visible en el grupo de medida que se hace referencia, EXISTS siempre devolverá un conjunto vacío, independientemente de los valores de *Set_Expression1* y *Set_Expression2*.  
  
## <a name="examples"></a>Ejemplos  
 Clientes que viven en California:  
  
```  
SELECT [Measures].[Internet Sales Amount] ON 0,  
EXISTS(  
[Customer].[Customer].[Customer].MEMBERS  
, {[Customer].[State-Province].&[CA]&[US]}  
) ON 1   
FROM [Adventure Works]  
  
```  
  
 Clientes que viven en California con ventas:  
  
```  
SELECT [Measures].[Internet Sales Amount] ON 0,  
EXISTS(  
[Customer].[Customer].[Customer].MEMBERS  
, {[Customer].[State-Province].&[CA]&[US]}  
, "Internet Sales") ON 1   
FROM [Adventure Works]  
  
```  
  
 Clientes con ventas:  
  
```  
SELECT [Measures].[Internet Sales Amount] ON 0,  
EXISTS(  
[Customer].[Customer].[Customer].MEMBERS  
, , "Internet Sales") ON 1   
FROM [Adventure Works]  
  
```  
  
 Clientes que compraron bicicletas:  
  
```  
SELECT [Measures].[Internet Sales Amount] ON 0,  
EXISTS(  
[Customer].[Customer].[Customer].MEMBERS  
, {[Product].[Product Categories].[Category].&[1]}  
, "Internet Sales") ON 1   
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [Crossjoin &#40;MDX&#41;](../mdx/crossjoin-mdx.md)   
 [NonEmptyCrossjoin &#40;MDX&#41;](../mdx/nonemptycrossjoin-mdx.md)   
 [NonEmpty &#40;MDX&#41;](../mdx/nonempty-mdx.md)   
 [IsEmpty &#40;MDX&#41;](../mdx/isempty-mdx.md)  
  
  
