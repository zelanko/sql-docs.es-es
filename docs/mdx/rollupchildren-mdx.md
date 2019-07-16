---
title: RollupChildren (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 89f7545af0d98de2a6bd97630a893057aac36b12
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68037049"
---
# <a name="rollupchildren-mdx"></a>RollupChildren (MDX)


  Devuelve un valor generado mediante la acumulación de los valores de los elementos secundarios de un miembro especificado, utilizando el operador unario especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
RollupChildren(Member_Expression, Unary_Operator)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Expresión MDX válida que devuelve un miembro.  
  
 *Unary_Operator*  
 Expresión de cadena válida que especifica un operador unario.  
  
## <a name="remarks"></a>Comentarios  
 El **RollupChildren** función acumula los valores de los elementos secundarios del miembro especificado mediante el operador unario especificado.  
  
 La tabla siguiente describe los operadores unarios válidos para esta función.  
  
|Operador|Resultado|  
|--------------|------------|  
|**+**|total = total + elemento secundario actual|  
|**-**|total = total - elemento secundario actual|  
|**\***|total = total * elemento secundario actual|  
|**/**|total = total / elemento secundario actual|  
|**%**|total = (total / elemento secundario actual) * 100|  
|**~**|El elemento secundario no se usa en el paquete acumulativo de actualizaciones. Se ignora su valor.|  
  
 Si el operador de la propiedad del miembro no aparece en la lista, se produce un error. El orden de evaluación se determina por el orden de los miembros del mismo nivel, no por la precedencia de los operadores.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente utiliza una propiedad de miembro denominada "Alternate Rollup Operator" que contiene valores alternativos para los operadores unarios a fin de integrar los elementos secundarios de la jerarquía Net Profit en la dimensión Account de manera alternativa. Esta propiedad de miembro no existe en el cubo Adventure Works, pero se puede crear. Este uso de la **RollupChildren** función podría usarse en una aplicación de elaboración de presupuestos para análisis de hipótesis.  
  
```  
RollupChildren  
   ( [Account].[Net Profit]  
   , [Account].CurrentMember.Properties ('Alternate Rollup Operator') )  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
