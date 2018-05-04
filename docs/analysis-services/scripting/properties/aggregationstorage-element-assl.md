---
title: Elemento AggregationStorage (ASSL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- AggregationStorage Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- AggregationStorage
helpviewer_keywords:
- AggregationStorage element
ms.assetid: dd082388-534d-4847-9232-8f80fc9fe96e
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: b629e033c5ce4985a2af5a8f244b8c34e8c9e780
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="aggregationstorage-element-assl"></a>Elemento AggregationStorage (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Identifica el método de almacenamiento para las agregaciones.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<ProactiveCaching>  
   ...  
   <AggregationStorage>...</AggregationStorage>  
   ...  
</ProactiveCaching>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|*Regular*|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El valor de este elemento se limita a una de las cadenas siguientes:  
  
|Value|Description|  
|-----------|-----------------|  
|*Regular*|Los datos de la agregación se almacenan de la manera predeterminada.|  
|*MolapOnly*|Los datos de agregación se almacenan utilizando solo almacenamiento OLAP (MOLAP) multidimensional.|  
  
 El *MolapOnly* opción sólo está disponible para el [partición](../../../analysis-services/scripting/objects/partition-element-assl.md) elemento.  
  
 La enumeración que corresponde a los valores permitidos para **AggregationStorage** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.ProactiveCachingAggregationStorage>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
