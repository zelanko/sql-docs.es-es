---
title: Elemento StatusGraphic (ASSL) | Documentos de Microsoft
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
- StatusGraphic Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- StatusGraphic
helpviewer_keywords:
- StatusGraphic element
ms.assetid: 14b365bc-924d-4791-ad4a-a38155fec42e
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d8c9b86e8f2940467231bc868e7dc1df0f8f62b1
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="statusgraphic-element-assl"></a>Elemento StatusGraphic (ASSL)
  Contiene la representación gráfica recomendada del estado de la [Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Kpi>  
   ...  
   <StatusGraphic>...</StatusGraphic>  
   ...  
</Kpi>  
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
|Elemento primario|[KPI](../../../analysis-services/scripting/objects/kpi-element-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Semáforo - único*|Semáforo (único)|  
|*Semáforo - varios*|Semáforo (varios)|  
|*Señales viales*|Señales viales|  
|*Medidor - ascendente*|Medidor|  
|*Medidor - descendente*|Medidor invertido|  
|*Termómetro*|Termómetro|  
|*Cilindro*|Cilindro|  
|*Cara sonriente*|Cara|  
  
 El elemento que corresponde al elemento primario de **StatusGraphic** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.Kpi>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

