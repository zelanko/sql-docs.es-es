---
title: "Instrucción CREATE MEASURE (MDX) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: f264ba96-cbbe-488b-8ac9-b3056a6e997b
caps.latest.revision: "5"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: f460d60ee1291651e157e5618fcfa4772920d2ad
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="mdx-data-definition---create-measure"></a>Definición de datos MDX - crear medida
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

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
  
## <a name="remarks"></a>Comentarios  
 El *Measure_Name* debe ir entre corchetes.  
  
 La instrucción CREATE MEASURE solo puede usarse dentro de una definición de script MDX; vea [MdxScript, elemento &#40; ASSL &#41; ](../analysis-services/scripting/objects/mdxscript-element-assl.md).  
  
 También puede definir un miembro calculado para su uso en una sola consulta. Para definir un miembro calculado limitado a una sola consulta, use la cláusula WITH de la instrucción SELECT. Para obtener más información, consulte [generar medidas en MDX](../analysis-services/multidimensional-models/mdx/mdx-building-measures.md).  
  
## <a name="see-also"></a>Vea también  
 [Instrucciones de definición de datos MDX &#40; MDX &#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
