---
title: Valor de elemento (ASSL) | Documentos de Microsoft
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
- Value Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Value
helpviewer_keywords:
- Value element
ms.assetid: a2fad411-73fd-42df-b4e1-df2cb8454182
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: f350c559e78613df5e0a357b8f87dca073e1d248
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36113897"
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
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Valor predeterminado|None|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
|Antecesor o elemento primario|Tipo de datos|  
|------------------------|---------------|  
|[AlgorithmParameter](../objects/algorithmparameter-element-assl.md)|Cualquier simpleType|  
|[ServerProperty](../objects/serverproperty-element-assl.md)|Cualquier simpleType|  
|Todos las demás|String|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[AlgorithmParameter](../objects/algorithmparameter-element-assl.md), [anotación](../objects/annotation-element-assl.md), [Kpi](../objects/kpi-element-assl.md), [ReportFormatParameter](../objects/reportformatparameter-element-asl.md), [ReportParameter](../objects/reportparameter-element-assl.md), [ServerProperty](../objects/serverproperty-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El elemento `Value` contiene el valor asociado al objeto primario. El valor esperado del elemento `Value` varía en función del elemento primario, como se describe en la tabla siguiente.  
  
|Elemento primario|Valor esperado|  
|--------------------|--------------------|  
|[AlgorithmParameter](../objects/algorithmparameter-element-assl.md)|Valor del parámetro de algoritmo.|  
|[Anotación](../objects/annotation-element-assl.md)|Valor de la anotación.|  
|[KPI](../objects/kpi-element-assl.md)|Expresión de Expresiones multidimensionales (MDX) utilizada para calcular el valor del indicador de rendimiento clave (KPI).|  
|[ReportFormatParameter](../objects/reportformatparameter-element-asl.md)|Valor del parámetro de formato del informe.|  
|[ReportParameter](../objects/reportparameter-element-assl.md)|Expresión MDX utilizada para calcular el valor del parámetro de informe.|  
|[ServerProperty](../objects/serverproperty-element-assl.md)|Valor de la propiedad del servidor para la instancia que se está ejecutando actualmente.|  
  
 Los elementos que corresponden a los elementos primarios de `Value` en el modelo de objetos de Objetos de administración de análisis (AMO) son <xref:Microsoft.AnalysisServices.AlgorithmParameter>, <xref:Microsoft.AnalysisServices.Annotation>, <xref:Microsoft.AnalysisServices.Kpi>, <xref:Microsoft.AnalysisServices.ReportParameter> y <xref:Microsoft.AnalysisServices.ServerProperty>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  