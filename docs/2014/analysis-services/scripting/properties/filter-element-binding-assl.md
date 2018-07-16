---
title: Elemento Filter (Binding) (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Filter Element (Binding)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- filter
helpviewer_keywords:
- Filter element
ms.assetid: 3d4cd169-2903-4266-8541-540ece424b7b
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ca1fe43bfe98061065cda1da5b1ff64772a4751d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37291311"
---
# <a name="filter-element-binding-assl"></a>Elemento Filter (Binding) (ASSL)
  Contiene una expresión MDX (Expresiones multidimensionales) que filtra el contenido del elemento primario.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<CubeDimensionBinding> <!-- or MeasureGroupBinding -->  
   ...  
   <Filter>...</Filter>  
   ...  
</CubeDimensionBinding>  
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
|Elementos primarios|[CubeDimensionBinding](../data-type/binding-data-type-assl.md), [MeasureGroupBinding](../data-type/measuregroupbinding-data-type-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 Para obtener más información sobre la `Binding` tipo, incluidas las tablas de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] objetos de Scripting Language (ASSL) de la `Binding` tipo y la jerarquía de herencia de `Binding` tipos, vea [tipo de datos de enlace &#40;ASSL &#41;](../data-type/binding-data-type-assl.md).  
  
 Para obtener información general de los enlaces de datos en ASSL, vea [orígenes de datos y enlaces &#40;Multidimensional de SSAS&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 Los elementos que corresponden a los elementos primarios de `Filter` en el modelo de objetos de Analysis Management Objects (AMO) son <xref:Microsoft.AnalysisServices.CubeDimensionBinding> y <xref:Microsoft.AnalysisServices.MeasureGroupBinding>.  
  
## <a name="see-also"></a>Vea también  
 [Tipo de datos Binding &#40;ASSL&#41;](../data-type/binding-data-type-assl.md)   
 [Orígenes de datos y enlaces &#40;SSAS Multidimensional&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)   
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
