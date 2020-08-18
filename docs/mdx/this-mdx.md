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
ms.openlocfilehash: e00435741516fd1ed1942506084c26192b6d47da
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88413101"
---
# <a name="this-mdx"></a>This (MDX)


  Devuelve el subcubo actual para su uso con las asignaciones del script de cálculo MDX (Expresiones multidimensionales).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
This   
```  
  
## <a name="remarks"></a>Observaciones  
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
 [Cálculos](https://docs.microsoft.com/analysis-services/multidimensional-models-olap-logical-cube-objects/calculations)  
  
  
