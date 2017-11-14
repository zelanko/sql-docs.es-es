---
title: Elemento GranularityAttributeID (ASSL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- GranularityAttributeID Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- GranularityAttributeID element
ms.assetid: 90e6c939-71bd-462a-a377-4854cb9d5266
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b6e374e6ea46b81fcf7e2cff4a9de4d254a9259d
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="granularityattributeid-element-assl"></a>Elemento GranularityAttributeID (ASSL)
  Contiene el identificador (ID) del atributo asociado al elemento primario [MeasureGroupAttributeBinding](../../../analysis-services/scripting/data-type/measuregroupattributebinding-data-type-out-of-line-assl.md) tipo de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<MeasureGroupAttributeBinding>  
   ...  
   <GranularityAttributeID>...</GranularityAttributeID>  
   ...  
</MeasureGroupAttributeBinding>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Cadena|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|1-1: Elemento requerido que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[MeasureGroupAttributeBinding](../../../analysis-services/scripting/data-type/measuregroupattributebinding-data-type-out-of-line-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 Para obtener más información acerca de los enlaces fuera de línea, consulte [orígenes de datos y enlaces &#40; SSAS Multidimensional &#41; ](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

