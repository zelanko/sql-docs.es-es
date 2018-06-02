---
title: LastPeriods (MDX) | Documentos de Microsoft
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 102382bf2acc2300d5862b48c5341c218e785275
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34578987"
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
  
## <a name="remarks"></a>Notas  
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
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
