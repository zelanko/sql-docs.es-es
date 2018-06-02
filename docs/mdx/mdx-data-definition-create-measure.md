---
title: Instrucción CREATE MEASURE (MDX) | Documentos de Microsoft
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 98ca479c266d9e8c25b2e75d8b15da1cd76a46aa
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34579357"
---
# <a name="mdx-data-definition---create-measure"></a>Definición de datos MDX - crear medida
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Crea una medida en un modelo tabular.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
CREATE MEASURE Table_Name[Measure_Name] = DAX_Expression  
[; CREATE MEASURE ...n]  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *Table_name*  
 Literal de cadena válido que proporciona el nombre de la tabla donde se creará la medida.  
  
 *Measure_Name*  
 Literal de cadena válida que proporciona un nombre de medida.  
  
 *DAX_Expression*  
 Expresión DAX válida que devuelve un solo valor escalar.  
  
## <a name="remarks"></a>Notas  
 El *Measure_Name* debe ir entre corchetes.  
  
 La instrucción CREATE MEASURE solo puede usarse dentro de una definición de script MDX; vea [elemento MdxScript &#40;ASSL&#41;](../analysis-services/scripting/objects/mdxscript-element-assl.md).  
  
 También puede definir un miembro calculado para su uso en una sola consulta. Para definir un miembro calculado limitado a una sola consulta, use la cláusula WITH de la instrucción SELECT. Para obtener más información, consulte [generar medidas en MDX](../analysis-services/multidimensional-models/mdx/mdx-building-measures.md).  
  
## <a name="see-also"></a>Vea también  
 [Instrucciones de definición de datos MDX &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
