---
title: ParallelPeriod (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b4122c13a5371cc0ffe1c5c6235ad750e7fdadad
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68020702"
---
# <a name="parallelperiod-mdx"></a>ParallelPeriod (MDX)


  Devuelve un miembro de un periodo anterior en la misma posición relativa que el indicado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
ParallelPeriod( [ Level_Expression [ ,Index [ , Member_Expression ] ] ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Level_Expression*  
 Expresión MDX válida que devuelve un nivel.  
  
 *Ajustar*  
 Expresión numérica válida que especifica el número de períodos paralelos que se van a retrasar.  
  
 *Member_Expression*  
 Expresión MDX válida que devuelve un miembro.  
  
## <a name="remarks"></a>Observaciones  
 Aunque es similar a la función [primo](../mdx/cousin-mdx.md) , la función **ParallelPeriod** está más estrechamente relacionada con la serie temporal. La función **ParallelPeriod** toma el antecesor del miembro especificado en el nivel especificado, busca el elemento relacionado del antecesor con el intervalo especificado y, por último, devuelve el período paralelo del miembro especificado entre los descendientes del elemento relacionado.  
  
 La función **ParallelPeriod** tiene los siguientes valores predeterminados:  
  
-   Si no se especifica una expresión de nivel ni una expresión de miembro, el valor de miembro predeterminado es el miembro actual de la primera jerarquía de la primera dimensión con un tipo de *tiempo* en el grupo de medida.  
  
-   Si se especifica una expresión de nivel, pero no se especifica una expresión de miembro, el valor de miembro predeterminado es *Level_Expression*. **Hierarchy. CurrentMember**.  
  
-   El valor de índice predeterminado es 1.  
  
-   El nivel predeterminado es el nivel del elemento primario del miembro especificado.  
  
 La función **ParallelPeriod** es equivalente a la siguiente instrucción MDX:  
  
 `Cousin(Member_Expression, Ancestor(Member_Expression, Level_Expression) .Lag(Numeric_Expression))`  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve el período paralelo del mes de octubre de 2003 con un retraso de tres períodos, de acuerdo con el nivel de trimestre, que devuelve el mes de enero de 2003.  
  
```  
SELECT ParallelPeriod ([Date].[Calendar].[Calendar Quarter]  
   , 3  
   , [Date].[Calendar].[Month].[October 2003])  
   ON 0  
   FROM [Adventure Works]  
```  
  
 El ejemplo siguiente devuelve el período paralelo del mes de octubre de 2003 con un retraso de tres períodos, de acuerdo con el nivel de semestre, que devuelve el mes de abril de 2002.  
  
```  
SELECT ParallelPeriod ([Date].[Calendar].[Calendar Semester]  
   , 3  
   , [Date].[Calendar].[Month].[October 2003])  
   ON 0  
   FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
