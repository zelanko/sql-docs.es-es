---
title: Valor de elemento (ASSL) | Documentos de Microsoft
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
apiname: Value Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Value
helpviewer_keywords: Value element
ms.assetid: a2fad411-73fd-42df-b4e1-df2cb8454182
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: eda952daf69b54246aa095fde0c187adfbbbc5e0
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="value-element-assl"></a>Elemento Value (ASSL)
  Contiene el valor del elemento primario.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<AlgorithmParameter> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <Value>...</Value>  
   ...  
</AlgorithmParameter>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Vea la siguiente tabla.|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
|Antecesor o elemento primario|Tipo de datos|  
|------------------------|---------------|  
|[AlgorithmParameter](../../../analysis-services/scripting/objects/algorithmparameter-element-assl.md)|Cualquier simpleType|  
|[ServerProperty](../../../analysis-services/scripting/objects/serverproperty-element-assl.md)|Cualquier simpleType|  
|Todos los demás|String|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[AlgorithmParameter](../../../analysis-services/scripting/objects/algorithmparameter-element-assl.md), [anotación](../../../analysis-services/scripting/objects/annotation-element-assl.md), [Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md), [ReportFormatParameter](../../../analysis-services/scripting/objects/reportformatparameter-element-asl.md), [ReportParameter](../../../analysis-services/scripting/objects/reportparameter-element-assl.md), [ServerProperty](../../../analysis-services/scripting/objects/serverproperty-element-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El **valor** elemento contiene el valor asociado con el objeto primario. El valor esperado de la **valor** elemento varía en función del elemento primario, tal como se describe en la tabla siguiente.  
  
|Elemento primario|Valor esperado|  
|--------------------|--------------------|  
|[AlgorithmParameter](../../../analysis-services/scripting/objects/algorithmparameter-element-assl.md)|Valor del parámetro de algoritmo.|  
|[Anotación](../../../analysis-services/scripting/objects/annotation-element-assl.md)|Valor de la anotación.|  
|[KPI](../../../analysis-services/scripting/objects/kpi-element-assl.md)|Expresión de Expresiones multidimensionales (MDX) utilizada para calcular el valor del indicador de rendimiento clave (KPI).|  
|[ReportFormatParameter](../../../analysis-services/scripting/objects/reportformatparameter-element-asl.md)|Valor del parámetro de formato del informe.|  
|[ReportParameter](../../../analysis-services/scripting/objects/reportparameter-element-assl.md)|Expresión MDX utilizada para calcular el valor del parámetro de informe.|  
|[ServerProperty](../../../analysis-services/scripting/objects/serverproperty-element-assl.md)|Valor de la propiedad del servidor para la instancia que se está ejecutando actualmente.|  
  
 Los elementos que corresponden a los elementos primarios de **valor** en el modelo de objetos de Analysis Management Objects (AMO) son <xref:Microsoft.AnalysisServices.AlgorithmParameter>, <xref:Microsoft.AnalysisServices.Annotation>, <xref:Microsoft.AnalysisServices.Kpi>, <xref:Microsoft.AnalysisServices.ReportParameter>, y <xref:Microsoft.AnalysisServices.ServerProperty>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
