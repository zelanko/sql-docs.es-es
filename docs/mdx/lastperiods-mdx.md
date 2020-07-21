---
title: LastPeriods (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6a9337e925da40f148bbe0d2c77fb1cf4f5f1a99
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "67905784"
---
# <a name="lastperiods-mdx"></a>LastPeriods (MDX)


  Devuelve un conjunto de miembros hasta un miembro determinado, éste inclusive.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
LastPeriods(Index [ ,Member_Expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Índice*  
 Expresión numérica válida que especifica un número de períodos.  
  
 *Member_Expression*  
 Expresión MDX válida que devuelve un miembro.  
  
## <a name="remarks"></a>Observaciones  
 Si el número especificado de períodos es positivo, la función **LastPeriods** devuelve un conjunto de miembros que comienzan con el miembro que retrasa el *Índice* -1 de la expresión de miembro especificada y termina con el miembro especificado. El número de miembros devueltos por la función es igual al *Índice*.  
  
 Si el número especificado de períodos es negativo, la función **LastPeriods** devuelve un conjunto de miembros que comienzan con el miembro especificado y terminan con el miembro que conduce (- *index* -1) desde el miembro especificado. El número de miembros devueltos por la función es igual al valor absoluto de *index*.  
  
 Si el número especificado de períodos es cero, la función **LastPeriods** devuelve el conjunto vacío. Esto no es lo mismo que la función **lag** , que devuelve el miembro especificado si se especifica 0.  
  
 Si no se especifica un miembro, la función **LastPeriods** utiliza **Time. CurrentMember**. Si no se marca una dimensión como dimensión de tiempo, la función se analizará y ejecutará sin errores, pero se producirá un error de celda en la aplicación cliente.  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
