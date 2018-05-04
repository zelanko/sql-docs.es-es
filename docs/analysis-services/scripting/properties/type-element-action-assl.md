---
title: Tipo de elemento (Action) (ASSL) | Documentos de Microsoft
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
ms.openlocfilehash: a9c09141417b613661f0ca6b0ca1d8bbc393de0f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="type-element-action-assl"></a>Elemento Type (Action) (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
|*dirección URL*|Muestra una página variable en un explorador de Internet.|  
|*HTML*|Ejecuta un script HTML en un explorador de Internet.|  
|*Estamento*|Ejecuta un comando de OLE DB.|  
|*Obtención de detalles*|Recupera un conjunto de filas para obtener detalles.<br /><br /> Este valor es idéntico a *conjunto de filas* e identifica acciones de obtención de detalles. Sólo se puede utilizar en acciones cuyo [TargetType](../../../analysis-services/scripting/properties/targettype-element-assl.md) valor se establece en *celdas*.|  
|*conjunto de datos*|Recupera un conjunto de datos.|  
|*Conjunto de filas*|Recupera un conjunto de filas.|  
|*Línea de comandos*|Ejecuta un comando en un símbolo del sistema.|  
|*Propietario*|Realiza una operación mediante una interfaz distinta de las descritas previamente en esta tabla.|  
|*Informe*|Muestra una página variable en un explorador de Internet.<br /><br /> Este valor es idéntico a *Url* e identifica acciones de informe.|  
  
 El elemento que corresponde al elemento primario de **tipo** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.Action>.  
  
## <a name="see-also"></a>Vea también  
 [Tipo de Drillthroughaction &#40;ASSL&#41;](../../../analysis-services/scripting/data-type/drillthroughaction-data-type-assl.md)   
 [Tipo de datos ReportAction &#40;ASSL&#41;](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md)   
 [Propiedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
