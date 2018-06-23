---
title: Elemento KpiID (ASSL) | Documentos de Microsoft
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
- KpiID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- KpiID
helpviewer_keywords:
- KpiID element
ms.assetid: a76395bc-bc84-40f8-9770-6275842f93b5
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 03bbebbf255b5f42934d4fe1e28c78cc1bb54caf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36111228"
---
# <a name="kpiid-element-assl"></a>Elemento KpiID (ASSL)
  Contiene un identificador (ID) que asocia un [Kpi](../objects/kpi-element-assl.md) elemento con un [perspectiva](../objects/perspective-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<PerspectiveKpi>  
      ...  
   <KpiID>...</KpiID>  
   ...  
</PerspectiveKpi>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String|  
|Valor predeterminado|None|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[PerspectiveKpi](../data-type/perspectivekpi-data-type-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El elemento que corresponde al elemento primario de `KpiID` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.PerspectiveKpi>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades (ASSL)](properties-assl.md)  
  
  