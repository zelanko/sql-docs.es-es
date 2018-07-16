---
title: Elemento DefaultMeasure (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- DefaultMeasure Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DefaultMeasure
helpviewer_keywords:
- DefaultMeasure element
ms.assetid: ceac8b3d-ebae-463f-9e8c-506281d42792
caps.latest.revision: 35
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6650ad99a21a4c2628e94e483c4cd2947d240bc8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37314645"
---
# <a name="defaultmeasure-element-assl"></a>Elemento DefaultMeasure (ASSL)
  Contiene una expresión MDX (expresiones multidimensionales) que define la medida predeterminada para un [cubo](../objects/cube-element-assl.md) o [perspectiva](../objects/perspective-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Cube> <!-- or Perspective -->  
   ...  
   <DefaultMeasure>...</DefaultMeasure>  
   ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[Cubo](../objects/cube-element-assl.md), [perspectiva](../objects/perspective-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 Los elementos que corresponden a los elementos primarios de `DefaultMeasure` en el modelo de objetos de Analysis Management Objects (AMO) son <xref:Microsoft.AnalysisServices.Cube> y <xref:Microsoft.AnalysisServices.Perspective>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
