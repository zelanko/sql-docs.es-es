---
title: Elemento DependsOnDimensionID (ASSL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DependsOnDimensionID Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- DependsOnDimensionID
helpviewer_keywords:
- DependsOnDimensionID element
ms.assetid: 66ec20dd-b475-4895-a92c-7ac0e7e1c675
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ace71b2fe51a5699f18a726576984ceb9e49c127
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="dependsondimensionid-element-assl"></a>Elemento DependsOnDimensionID (ASSL)
  Contiene el identificador (Id.) de otra dimensión de la que depende la dimensión primaria.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Dimension>  
      ...  
   <DependsOnDimensionID>...</DependsOnDimensionID>  
   ...  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Cadena|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Dimension](../../../analysis-services/scripting/objects/dimension-element-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 Una dimensión dependiente utiliza el elemento **DependsOnDimensionID** para identificar la dimensión de la que depende.  
  
 El elemento que corresponde al elemento primario de **DependsOnDimensionID** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.Dimension>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

