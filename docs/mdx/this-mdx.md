---
description: This (MDX)
title: This (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b55a416a14d0b837d134e7f9d8520d77cc13e375
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/19/2020
ms.locfileid: "92192335"
---
# <a name="this-mdx"></a>This (MDX)


  Devuelve el subcubo actual para su uso con las asignaciones del script de cálculo MDX (Expresiones multidimensionales).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
This   
```  
  
## <a name="remarks"></a>Comentarios  
 **Esta** función se puede usar en lugar de cualquier expresión de subcubo para proporcionar el subcubo actual dentro del ámbito actual dentro del script de cálculo MDX. **Esta** función debe usarse en el lado izquierdo de una asignación.  
  
## <a name="examples"></a>Ejemplos  
 El siguiente fragmento de script MDX muestra el modo de usar la palabra clave This con instrucciones SCOPE para realizar asignaciones a subcubos:  
  
 `Scope`  
  
 `(`  
  
 `[Date].[Fiscal Year].&[2005],`  
  
 `[Date].[Fiscal].[Fiscal Quarter].Members,`  
  
 `[Measures].[Sales Amount Quota]`  
  
 `) ;`  
  
 `This = ParallelPeriod`  
  
 `(`  
  
 `[Date].[Fiscal].[Fiscal Year], 1,`  
  
 `[Date].[Fiscal].CurrentMember`  
  
 `) * 1.35 ;`  
  
 `/*-- Allocate equally to months in FY 2002 -----------------------------*/`  
  
 `Scope`  
  
 `(`  
  
 `[Date].[Fiscal Year].&[2002],`  
  
 `[Date].[Fiscal].[Month].Members`  
  
 `) ;`  
  
 `This = [Date].[Fiscal].CurrentMember.Parent / 3 ;`  
  
 `End Scope ;`  
  
 `End Scope;`  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [Cálculos](/analysis-services/multidimensional-models-olap-logical-cube-objects/calculations)  
  
