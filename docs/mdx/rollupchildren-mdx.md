---
description: RollupChildren (MDX)
title: RollupChildren (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: fb4e3552b5c5f5a708a70754d816ab1a78008248
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88341321"
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
  
## <a name="remarks"></a>Observaciones  
 La función **RollupChildren** acumula los valores de los elementos secundarios del miembro especificado mediante el operador unario especificado.  
  
 La tabla siguiente describe los operadores unarios válidos para esta función.  
  
|Operador|Resultado|  
|--------------|------------|  
|**+**|total = total + elemento secundario actual|  
|**-**|total = total - elemento secundario actual|  
|**\***|total = total * elemento secundario actual|  
|**/**|total = total / elemento secundario actual|  
|**%**|total = (total / elemento secundario actual) * 100|  
|**~**|El elemento secundario no se utiliza en el resumen. Se ignora su valor.|  
  
 Si el operador de la propiedad del miembro no aparece en la lista, se produce un error. El orden de evaluación se determina por el orden de los miembros del mismo nivel, no por la precedencia de los operadores.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente utiliza una propiedad de miembro denominada "Alternate Rollup Operator" que contiene valores alternativos para los operadores unarios a fin de integrar los elementos secundarios de la jerarquía Net Profit en la dimensión Account de manera alternativa. Esta propiedad de miembro no existe en el cubo Adventure Works, pero se puede crear. Este uso de la función **RollupChildren** podría usarse en una aplicación de presupuesto para el análisis de supuestos.  
  
```  
RollupChildren  
   ( [Account].[Net Profit]  
   , [Account].CurrentMember.Properties ('Alternate Rollup Operator') )  
```  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
