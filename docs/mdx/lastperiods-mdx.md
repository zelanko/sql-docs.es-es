---
title: LastPeriods (MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: LASTPERIODS
dev_langs: kbMDX
helpviewer_keywords: LastPeriods function
ms.assetid: a15df7a1-b261-48ed-aacc-d2804db8dbf7
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 7b5f43547cdf6a48a35e2a433dcc7a82cdabe054
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2017
---
# <a name="lastperiods-mdx"></a>LastPeriods (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve un conjunto de miembros hasta un miembro determinado, éste inclusive.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
LastPeriods(Index [ ,Member_Expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Index*  
 Expresión numérica válida que especifica un número de períodos.  
  
 *Expresión_miembro*  
 Expresión MDX válida que devuelve un miembro.  
  
## <a name="remarks"></a>Comentarios  
 Si el número especificado de períodos es positivo, el **LastPeriods** función devuelve un conjunto de miembros que se inicia con el miembro final *índice* -1 de la expresión de miembro especificado y termina con el miembro especificado. El número de miembros devueltos por la función es igual a *índice*.  
  
 Si el número especificado de períodos es negativo, el **LastPeriods** función devuelve un conjunto de miembros que se inicia con el miembro especificado y termina con el miembro inicial (- *índice* - 1) desde el miembro especificado. El número de miembros devueltos por la función es igual al valor absoluto de *índice*.  
  
 Si el número especificado de períodos es cero, el **LastPeriods** función devuelve un conjunto vacío. Esto es diferente a la **Lag** función, que devuelve el miembro especificado si se especifica 0.  
  
 Si no se especifica un miembro, el **LastPeriods** función utiliza **Time.CurrentMember**. Si no se marca una dimensión como dimensión de tiempo, la función se analizará y ejecutará sin errores, pero se producirá un error de celda en la aplicación cliente.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve el valor de medida predeterminado para el segundo, tercero y cuarto trimestres fiscales del año fiscal 2002.  
  
```  
SELECT LastPeriods(3,[Date].[Fiscal].[Fiscal Quarter].[Q4 FY 2002]) ON 0  
FROM [Adventure Works]  
```  
  
> [!NOTE]  
>  Este ejemplo también se puede escribir mediante el operador : (dos puntos):  
>   
>  `[Date].[Fiscal].[Fiscal Quarter].[Q4 FY 2002]: [Date].[Fiscal].[Fiscal Quarter].[Q2 FY 2002]`  
  
 En el ejemplo siguiente se devuelve el valor de la medida predeterminada correspondiente al primer trimestre del año fiscal 2002. Aunque el número especificado de períodos es tres, solo se puede devolver uno porque no hay períodos anteriores del año fiscal.  
  
```  
SELECT LastPeriods  
   (3,[Date].[Fiscal].[Fiscal Quarter].[Q1 FY 2002]  
   ) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
