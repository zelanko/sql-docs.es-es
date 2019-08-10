---
title: Exists (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ba2cef1cfb95319cbe0aff827cb251ff7e2317c2
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893612"
---
# <a name="exists-mdx"></a>Exists (MDX)


  Devuelve el conjunto de tuplas del primer conjunto especificado que existe con una o más tuplas del segundo conjunto especificado. Esta función realiza manualmente lo que Autoexist realiza automáticamente. Para obtener más información acerca de autoexists, consulte [conceptos &#40;clave&#41;en MDX Analysis Services](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services).  
  
 Si se proporciona \<el nombre de grupo de medida opcional >, la función devuelve tuplas que existen con una o más tuplas del segundo conjunto y las tuplas que tienen asociadas filas en la tabla de hechos del grupo de medida especificado.  
  
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
  
## <a name="remarks"></a>Comentarios  
  
1.  Las filas del grupo de medida con medidas que contengan valores NULL contribuyen a **EXISTS** cuando se especifica el argumento MeasureGroupName. Esta es la diferencia entre esta forma de EXISTS y la función NonEmpty: Si la propiedad NullProcessing de estas medidas está establecida en preserve, esto significa que las medidas mostrarán valores NULL cuando las consultas se ejecuten en esa parte del cubo. NonEmpty siempre quitará las tuplas de un conjunto que tengan valores de medida null, mientras que EXISTS con el argumento MeasureGroupName no filtrará las tuplas que tengan asociadas filas de grupo de medida, aunque los valores de medida sean null.  
  
2.  Si se usa el parámetro *MeasureGroupName* , los resultados dependerán de si hay medidas visibles en el grupo de medida al que se hace referencia. Si no hay ninguna medida visible en el grupo de medida al que se hace referencia, EXISTs siempre devolverá un conjunto vacío, independientemente de los valores de *Set_Expression1* y *Set_Expression2*.  
  
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
 [MDX &#40;de Crossjoin&#41;](../mdx/crossjoin-mdx.md)   
 [NonEmptyCrossjoin &#40;MDX&#41;](../mdx/nonemptycrossjoin-mdx.md)   
 [MDX no &#40;vacío&#41;](../mdx/nonempty-mdx.md)   
 [IsEmpty &#40;(MDX)&#41;](../mdx/isempty-mdx.md)  
  
  
