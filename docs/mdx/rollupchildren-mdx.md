---
title: RollupChildren (MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ROLLUPCHILDREN
dev_langs:
- kbMDX
helpviewer_keywords:
- RollupChildren function
ms.assetid: 6f092540-067d-443f-b631-8523836a0d86
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b29a351d8425d235adc29b8a5b997915b70de047
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="rollupchildren-mdx"></a>RollupChildren (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve un valor generado mediante la acumulación de los valores de los elementos secundarios de un miembro especificado, utilizando el operador unario especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
RollupChildren(Member_Expression, Unary_Operator)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Expresión_miembro*  
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
|**~**|El elemento secundario no se utiliza en el paquete acumulativo de actualizaciones. Se ignora su valor.|  
  
 Si el operador de la propiedad del miembro no aparece en la lista, se produce un error. El orden de evaluación se determina por el orden de los miembros del mismo nivel, no por la precedencia de los operadores.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente utiliza una propiedad de miembro denominada "Alternate Rollup Operator" que contiene valores alternativos para los operadores unarios a fin de integrar los elementos secundarios de la jerarquía Net Profit en la dimensión Account de manera alternativa. Esta propiedad de miembro no existe en el cubo Adventure Works, pero se puede crear. Este uso de la **RollupChildren** función podría usarse en una aplicación de elaboración de presupuestos para análisis de escenarios condicionales.  
  
```  
RollupChildren  
   ( [Account].[Net Profit]  
   , [Account].CurrentMember.Properties ('Alternate Rollup Operator') )  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

