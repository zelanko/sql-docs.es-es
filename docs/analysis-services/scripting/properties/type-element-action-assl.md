---
title: Tipo de elemento (Action) (ASSL) | Documentos de Microsoft
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: a82395be70c699da6fc96d3661aa71254e185883
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
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
  
  
