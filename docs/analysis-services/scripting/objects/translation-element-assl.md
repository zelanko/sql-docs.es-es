---
title: Elemento Translation (ASSL) | Documentos de Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 77080f970c951064d03b5e64042eecf7e2414520
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="translation-element-assl"></a>Elemento Translation (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Proporciona una traducción adaptada para el elemento primario de la colección [Translations](../../../analysis-services/scripting/collections/translations-element-assl.md) .  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Translations>  
   <Translation xsi:type="Translation">...</Translation>  
   <!-- or -->  
   <Translation xsi:type="AttributeTranslation">...</Translation>  
</Translations>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|[Translation](../../../analysis-services/scripting/data-type/translation-data-type-assl.md), [AttributeTranslation](../../../analysis-services/scripting/data-type/attributetranslation-data-type-assl.md)|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Traducciones](../../../analysis-services/scripting/collections/translations-element-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.Translation>.  
  
## <a name="see-also"></a>Vea también  
 [Objetos de & #40; ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
