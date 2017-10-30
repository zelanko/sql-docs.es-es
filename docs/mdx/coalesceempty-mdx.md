---
title: CoalesceEmpty (MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COALESCEEMPTY
dev_langs:
- kbMDX
helpviewer_keywords:
- CoalesceEmpty function
ms.assetid: c00dd739-44bc-4af6-9871-c7e1e3f3e5ba
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 9ce0754611a4662b88d5fba01828e2f0e08e63bd
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="coalesceempty-mdx"></a>CoalesceEmpty (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Convierte un valor de celda vacía en un valor de celda no vacía especificado que puede ser un número o una cadena.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Numeric syntax  
CoalesceEmpty( Numeric_Expression1 [ ,Numeric_Expression2,...n] )  
  
String syntax  
CoalesceEmpty(String_Expression1 [ ,String_Expression2,...n] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Numeric_Expression1*  
 Expresión numérica válida que suele ser una expresión MDX de las coordenadas de celdas que devuelven un número.  
  
 *Numeric_Expression2*  
 Expresión numérica válida que suele ser un valor numérico especificado.  
  
 *Expression1*  
 Expresión de cadena válida que suele ser una expresión MDX (Expresiones multidimensionales) de las coordenadas de celdas que devuelven una cadena.  
  
 *Expression2*  
 Expresión de cadena válida que suele ser un valor de cadena especificado sustituido por un valor NULL devuelto por la primera expresión de cadena.  
  
## <a name="remarks"></a>Comentarios  
 Si se especifican uno o más expresiones numéricas, la **CoalesceEmpty** función devuelve el valor numérico de la primera expresión numérica (de izquierda a derecha) que se pueda resolver como un valor no vacío. Si ninguna de las expresiones numéricas especificadas puede resolverse en un valor no vacío, la función devuelve el valor de la celda vacía. Normalmente, el valor de la segunda expresión numérica es el valor numérico sustituido por un valor NULL devuelto por la primera expresión numérica.  
  
 Si se especifican una o más expresiones de cadena, la función devuelve el valor de cadena de la primera expresión de cadena (de izquierda a derecha) que puede resolverse en un valor no vacío. Si ninguna de las expresiones de cadena especificadas puede resolverse en un valor no vacío, la función devuelve el valor de la celda vacía. Normalmente, el valor de la segunda expresión de cadena es el valor de cadena sustituido por un valor NULL devuelto por la primera expresión de cadena.  
  
 El **CoalesceEmpty** función solo puede tomar valores del mismo tipo. Es decir, todas las expresiones de valor especificadas se deben evaluar solo como tipos de datos numéricos o un valor de celda vacía, o bien todas las expresiones de valor especificadas deben evaluar tipos de datos o un valor de celda vacía. Una sola llamada a esta función no puede incluir expresiones numéricas y de cadena.  
  
 Para obtener más información acerca de las celdas vacías, consulte la documentación de OLE DB.  
  
## <a name="example"></a>Ejemplo  
 El siguiente ejemplo se consulta la **Adventure Works** cubo. Este ejemplo devuelve la cantidad de pedido de cada producto y el porcentaje de cantidades de pedido por categoría. El **CoalesceEmpty** función garantiza que los valores null se representan como cero (0) al dar formato a los miembros calculados.  
  
```  
WITH   
   MEMBER [Measures].[Order Percent by Category] AS  
   CoalesceEmpty(   
      ([Product].[Product Categories].CurrentMember,  
        Measures.[Order Quantity]) /   
          (  
           Ancestor  
           ( [Product].[Product Categories].CurrentMember,   
             [Product].[Product Categories].[Category]  
           ), Measures.[Order Quantity]  
       ), 0  
   ), FORMAT_STRING='Percent'  
SELECT   
   {Measures.[Order Quantity],  
      [Measures].[Order Percent by Category]} ON COLUMNS,  
{[Product].[Product].Members} ON ROWS  
FROM [Adventure Works]  
WHERE {[Date].[Calendar Year].[Calendar Year].&[2003]}  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

