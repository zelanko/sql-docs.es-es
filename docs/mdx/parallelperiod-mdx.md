---
title: ParallelPeriod (MDX) | Documentos de Microsoft
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
- PARALLELPERIOD
dev_langs:
- kbMDX
helpviewer_keywords:
- ParallelPeriod function
ms.assetid: 9c87f5a6-5694-46f1-9890-bd9705190ea7
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: e85ecbaf3c413215cbe549da779f46ab567c3efb
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="parallelperiod-mdx"></a>ParallelPeriod (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve un miembro de un periodo anterior en la misma posición relativa que el indicado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
ParallelPeriod( [ Level_Expression [ ,Index [ , Member_Expression ] ] ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Level_Expression*  
 Expresión MDX válida que devuelve un nivel.  
  
 *Index*  
 Expresión numérica válida que especifica el número de períodos paralelos que se van a retrasar.  
  
 *Expresión_miembro*  
 Expresión MDX válida que devuelve un miembro.  
  
## <a name="remarks"></a>Comentarios  
 Aunque es similar a la [Cousin](../mdx/cousin-mdx.md) función, el **ParallelPeriod** función está más estrechamente relacionado con serie temporal. El **ParallelPeriod** función toma el antecesor del miembro especificado en el nivel especificado, busca el elemento del mismo nivel del antecesor con el intervalo especificado y por último, devuelve el período paralelo del miembro especificado entre los descendientes del nodo relacionado.  
  
 El **ParallelPeriod** función tiene los siguientes valores predeterminados:  
  
-   Si se especifica una expresión de nivel ni una expresión de miembro, el valor del miembro predeterminado es el miembro actual de la primera jerarquía en la primera dimensión con un tipo de *tiempo* en el grupo de medida.  
  
-   Si se especifica una expresión de nivel, pero no se especifica una expresión de miembro, el valor de miembro predeterminado es *Level_Expression*. **Hierarchy.CurrentMember**.  
  
-   El valor de índice predeterminado es 1.  
  
-   El nivel predeterminado es el nivel del elemento primario del miembro especificado.  
  
 El **ParallelPeriod** función es equivalente a la siguiente instrucción MDX:  
  
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
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
