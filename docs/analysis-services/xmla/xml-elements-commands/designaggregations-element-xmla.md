---
title: Elemento DesignAggregations (XMLA) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DesignAggregations Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#DesignAggregations
- microsoft.xml.analysis.designaggregations
- http://schemas.microsoft.com/analysisservices/2003/engine#DesignAggregations
helpviewer_keywords:
- DesignAggregations command
ms.assetid: 4c419dbc-7405-40aa-8ddd-6b46685a297d
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0a20166ec005068195d93ee22c40837213944445
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="designaggregations-element-xmla"></a>Elemento DesignAggregations (XMLA)
  Crea agregaciones para un diseño de agregaciones en una [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Command>  
   <DesignAggregations>  
      <Object>...</Object>  
      <Time>...</Time>  
      <Steps>...</Steps>  
      <Optimization>...</Optimization>  
      <Storage>...</Storage>  
      <Materialize>...</Materialize>  
      <Queries>...</Queries>  
   </DesignAggregations>  
</Command>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Ninguno|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|Elementos secundarios|[Materializar](../../../analysis-services/xmla/xml-elements-properties/materialize-element-xmla.md), [objeto](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md), [optimización](../../../analysis-services/xmla/xml-elements-properties/optimization-element-xmla.md), [consultas](../../../analysis-services/xmla/xml-elements-properties/queries-element-xmla.md), [pasos](../../../analysis-services/xmla/xml-elements-properties/steps-element-xmla.md), [almacenamiento](../../../analysis-services/xmla/xml-elements-properties/storage-element-xmla.md), [Tiempo](../../../analysis-services/xmla/xml-elements-properties/time-element-xmla.md)|  
  
## <a name="remarks"></a>Comentarios  
 El comando **DesignAggregations** se usa para generar definiciones de agregaciones almacenadas por un diseño de agregaciones. Un diseño de agregaciones se puede utilizar después para materializar las agregaciones para una partición y se puede reutilizar entre las particiones.  
  
## <a name="see-also"></a>Vea también  
 [Comandos &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  

