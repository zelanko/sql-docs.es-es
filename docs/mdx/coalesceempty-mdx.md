---
title: CoalesceEmpty (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f760220b02396591e684a83305111e487908d19b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68006305"
---
# <a name="coalesceempty-mdx"></a>CoalesceEmpty (MDX)


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
  
 *String_Expression1*  
 Expresión de cadena válida que suele ser una expresión MDX (Expresiones multidimensionales) de las coordenadas de celdas que devuelven una cadena.  
  
 *String_Expression2*  
 Expresión de cadena válida que suele ser un valor de cadena especificado sustituido por un valor NULL devuelto por la primera expresión de cadena.  
  
## <a name="remarks"></a>Observaciones  
 Si se especifican una o más expresiones numéricas, la función **CoalesceEmpty** devuelve el valor numérico de la primera expresión numérica (de izquierda a derecha) que puede resolverse en un valor que no esté vacío. Si ninguna de las expresiones numéricas especificadas puede resolverse en un valor no vacío, la función devuelve el valor de la celda vacía. Normalmente, el valor de la segunda expresión numérica es el valor numérico sustituido por un valor NULL devuelto por la primera expresión numérica.  
  
 Si se especifican una o más expresiones de cadena, la función devuelve el valor de cadena de la primera expresión de cadena (de izquierda a derecha) que puede resolverse en un valor no vacío. Si ninguna de las expresiones de cadena especificadas puede resolverse en un valor no vacío, la función devuelve el valor de la celda vacía. Normalmente, el valor de la segunda expresión de cadena es el valor de cadena sustituido por un valor NULL devuelto por la primera expresión de cadena.  
  
 La función **CoalesceEmpty** solo puede tomar valores del mismo tipo. Es decir, todas las expresiones de valor especificadas se deben evaluar solo como tipos de datos numéricos o un valor de celda vacía, o bien todas las expresiones de valor especificadas deben evaluar tipos de datos o un valor de celda vacía. Una sola llamada a esta función no puede incluir expresiones numéricas y de cadena.  
  
 Para obtener más información acerca de las celdas vacías, consulte la documentación de OLE DB.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se consulta el cubo **Adventure Works** . Este ejemplo devuelve la cantidad de pedido de cada producto y el porcentaje de cantidades de pedido por categoría. La función **CoalesceEmpty** garantiza que los valores NULL se representan como cero (0) al dar formato a los miembros calculados.  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
