---
title: Instrucción CREATE MEASURE (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 37a8b8ef757184e7467c3551148c8c149bb45097
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63309096"
---
# <a name="mdx-data-definition---create-measure"></a>Definición de datos de MDX: CREATE MEASURE


  Crea una medida en un modelo tabular.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
CREATE MEASURE Table_Name[Measure_Name] = DAX_Expression  
[; CREATE MEASURE ...n]  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *Table_Name*  
 Literal de cadena válido que proporciona el nombre de la tabla donde se creará la medida.  
  
 *Measure_Name*  
 Literal de cadena válida que proporciona un nombre de medida.  
  
 *DAX_Expression*  
 Expresión DAX válida que devuelve un solo valor escalar.  
  
## <a name="remarks"></a>Comentarios  
 El *Measure_Name* debe ir entre corchetes.  
  
 La instrucción CREATE MEASURE solo puede usarse dentro de una definición de la secuencia de comandos MDX; consulte [elemento MdxScript &#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/objects/mdxscript-element-assl).  
  
 También puede definir un miembro calculado para su uso en una sola consulta. Para definir un miembro calculado limitado a una sola consulta, use la cláusula WITH de la instrucción SELECT. Para obtener más información, consulte [generar medidas en MDX](../analysis-services/multidimensional-models/mdx/mdx-building-measures.md).  
  
## <a name="see-also"></a>Vea también  
 [Instrucciones de definición de datos MDX &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
