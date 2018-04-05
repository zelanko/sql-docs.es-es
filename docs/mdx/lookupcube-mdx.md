---
title: LookupCube (MDX) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- LOOKUPCUBE
dev_langs:
- kbMDX
helpviewer_keywords:
- LookupCube function
ms.assetid: 243fa101-328a-4016-86e0-d8b5977e15a9
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: a2b5e06839166528482a52fffc594d933a30ee57
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="lookupcube-mdx"></a>LookupCube (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve el valor de una expresión multidimensional (MDX) evaluada sobre otro cubo especificado en la misma base de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Numeric expression syntax  
LookupCube(Cube_Name, Numeric_Expression )  
  
String expression syntax  
LookupCube(Cube_Name, String_Expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Restricciones obligatorias Cube_Name*  
 Expresión de cadena válida que especifica el nombre de un cubo.  
  
 *Numeric_expression*  
 Expresión numérica válida que suele ser una expresión MDX de las coordenadas de celdas que devuelven un número.  
  
 *String_Expression*  
 Expresión de cadena válida que suele ser una expresión MDX (Expresiones multidimensionales) válida de las coordenadas de celdas que devuelven una cadena.  
  
## <a name="remarks"></a>Comentarios  
 Si se especifica una expresión numérica, la **LookupCube** función evalúa la expresión numérica especificada en el cubo especificado y devuelve el valor numérico resultante.  
  
 Si se especifica una expresión de cadena, la **LookupCube** función evalúa la expresión de cadena especificada en el cubo especificado y devuelve el valor de cadena resultante.  
  
 El **LookupCube** función funciona con cubos de la misma base de datos como el cubo de origen en el que la consulta de MDX que contiene el **LookupCube** función se está ejecutando.  
  
> [!IMPORTANT]  
>  Debe proporcionar los miembros actuales necesarios en la expresión numérica o de cadena debido a que el contexto de la consulta actual no se mantiene en el cubo que se consulta.  
  
 Los cálculos que usen la **LookupCube** función es probable que experimenten un bajo rendimiento. En lugar de utilizar esta función, considere volver a diseñar la solución para que todos los datos que necesite se encuentren en un cubo.  
  
## <a name="examples"></a>Ejemplos  
 En la consulta siguiente se muestra el uso de LookupCube:  
  
 `WITH MEMBER MEASURES.LOOKUPCUBEDEMO AS`  
  
 `LOOKUPCUBE("Adventure Works", "[Measures].[In" + "ternet Sales Amount]")`  
  
 `SELECT MEASURES.LOOKUPCUBEDEMO  ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
