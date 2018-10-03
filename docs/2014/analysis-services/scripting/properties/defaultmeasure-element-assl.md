---
title: Elemento DefaultMeasure (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f6bb86737fb90fe63d162a421e8627b99a92228d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48087945"
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
  
## <a name="element-characteristics"></a>Características de los elementos  
  
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
  
## <a name="remarks"></a>Comentarios  
 Los elementos que corresponden a los elementos primarios de `DefaultMeasure` en el modelo de objetos de Analysis Management Objects (AMO) son <xref:Microsoft.AnalysisServices.Cube> y <xref:Microsoft.AnalysisServices.Perspective>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
