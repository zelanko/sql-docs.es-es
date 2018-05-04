---
title: Tipo de datos CubeBinding (fuera de línea) (ASSL) | Documentos de Microsoft
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
- CubeBinding Data Type (out-of-line)
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- CubeBinding
helpviewer_keywords:
- CubeBinding data type
ms.assetid: 5e1ee8ef-855c-4f3d-ae21-a33360d00d66
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 63be7efbfbc6adc7b667ed3a7a57be67fedf0787
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="cubebinding-data-type-out-of-line-assl"></a>Tipo de datos CubeBinding (fuera de línea) (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Define un tipo de datos primitivo que representa la relación existente entre un elemento [Cube](../../../analysis-services/scripting/objects/cube-element-assl.md) y un elemento [DataSource](../../../analysis-services/scripting/objects/datasource-element-assl.md) .  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<CubeBinding>  
   <ID>...</ID>  
   <DataSourceID>...</DataSourceID>  
   <DataSource>...</DataSource>  
   <MeasureGroup>...</MeasureGroup>  
</CubeBinding>  
```  
  
## <a name="data-type-characteristics"></a>Características del tipo de datos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipos de datos base|Ninguno|  
|Tipos de datos derivados|Ninguno|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|Ninguno|  
|Elementos secundarios|[DataSource](../../../analysis-services/scripting/objects/datasource-element-assl.md), [DataSourceID](../../../analysis-services/scripting/properties/datasourceid-element-assl.md), [ID](../../../analysis-services/scripting/properties/id-element-assl.md), [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|  
|Elementos derivados|[Binding](../../../analysis-services/xmla/xml-elements-properties/binding-element-xmla.md) (colección[Bindings](../../../analysis-services/xmla/xml-elements-properties/bindings-element-xmla.md) de comandos [Process](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md) o [Batch](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md) )|  
  
## <a name="remarks"></a>Comentarios  
 Para obtener más información acerca de los enlaces fuera de línea, consulte [orígenes de datos y enlaces & #40; SSAS Multidimensional & #41; ](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
## <a name="see-also"></a>Vea también  
 [Tipo de enlace de datos & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)   
 [Analysis Services Scripting Language tipos de datos XML & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
