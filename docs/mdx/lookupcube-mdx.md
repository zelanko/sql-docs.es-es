---
title: LookupCube (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ec18b600c369de872df5f6eadf06ef6c30c88efa
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68098513"
---
# <a name="lookupcube-mdx"></a>LookupCube (MDX)


  Devuelve el valor de una expresión multidimensional (MDX) evaluada sobre otro cubo especificado en la misma base de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Numeric expression syntax  
LookupCube(Cube_Name, Numeric_Expression )  
  
String expression syntax  
LookupCube(Cube_Name, String_Expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Cube_Name*  
 Expresión de cadena válida que especifica el nombre de un cubo.  
  
 *Numeric_Expression*  
 Expresión numérica válida que suele ser una expresión MDX de las coordenadas de celdas que devuelven un número.  
  
 *String_Expression*  
 Expresión de cadena válida que suele ser una expresión MDX (Expresiones multidimensionales) válida de las coordenadas de celdas que devuelven una cadena.  
  
## <a name="remarks"></a>Observaciones  
 Si se especifica una expresión numérica, la función **LookupCube** evalúa la expresión numérica especificada en el cubo especificado y devuelve el valor numérico resultante.  
  
 Si se especifica una expresión de cadena, la función **LookupCube** evalúa la expresión de cadena especificada en el cubo especificado y devuelve el valor de cadena resultante.  
  
 La función **LookupCube** funciona en cubos dentro de la misma base de datos que el cubo de origen en el que se está ejecutando la consulta MDX que contiene la función **LookupCube** .  
  
> [!IMPORTANT]  
>  Debe proporcionar los miembros actuales necesarios en la expresión numérica o de cadena debido a que el contexto de la consulta actual no se mantiene en el cubo que se consulta.  
  
 Cualquier cálculo que utilice la función **LookupCube** es probable que se vea afectado por un bajo rendimiento. En lugar de utilizar esta función, considere volver a diseñar la solución para que todos los datos que necesite se encuentren en un cubo.  
  
## <a name="examples"></a>Ejemplos  
 En la consulta siguiente se muestra el uso de LookupCube:  
  
 `WITH MEMBER MEASURES.LOOKUPCUBEDEMO AS`  
  
 `LOOKUPCUBE("Adventure Works", "[Measures].[In" + "ternet Sales Amount]")`  
  
 `SELECT MEASURES.LOOKUPCUBEDEMO  ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
