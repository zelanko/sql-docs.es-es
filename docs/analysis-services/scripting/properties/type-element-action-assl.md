---
title: Tipo de elemento (Action) (ASSL) | Documentos de Microsoft
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
- Type Element (Action)
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- TYPE
helpviewer_keywords:
- Type element
ms.assetid: 534cdf99-1edf-4490-9eaa-61f189a19434
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 62735cdcc160bccf6b90ed2c26b269b8b3d1d3eb
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="type-element-action-assl"></a>Elemento Type (Action) (ASSL)
  Contiene el tipo de la [acción](../../../analysis-services/scripting/objects/action-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Action>  
   ...  
   <Type>...</Type>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[Acción](../../../analysis-services/scripting/objects/action-element-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Dirección URL*|Muestra una página variable en un explorador de Internet.|  
|*HTML*|Ejecuta un script HTML en un explorador de Internet.|  
|*Instrucción*|Ejecuta un comando de OLE DB.|  
|*Obtención de detalles*|Recupera un conjunto de filas para obtener detalles.<br /><br /> Este valor es idéntico a *conjunto de filas* e identifica acciones de obtención de detalles. Sólo se puede utilizar en acciones cuyo [TargetType](../../../analysis-services/scripting/properties/targettype-element-assl.md) valor se establece en *celdas*.|  
|*Conjunto de datos*|Recupera un conjunto de datos.|  
|*Conjunto de filas*|Recupera un conjunto de filas.|  
|*Línea de comandos*|Ejecuta un comando en un símbolo del sistema.|  
|*Propietario*|Realiza una operación mediante una interfaz distinta de las descritas previamente en esta tabla.|  
|*Informe*|Muestra una página variable en un explorador de Internet.<br /><br /> Este valor es idéntico a *Url* e identifica acciones de informe.|  
  
 El elemento que corresponde al elemento primario de **tipo** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.Action>.  
  
## <a name="see-also"></a>Vea también  
 [Tipo de Drillthroughaction &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/drillthroughaction-data-type-assl.md)   
 [Tipo de datos ReportAction &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md)   
 [Propiedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

