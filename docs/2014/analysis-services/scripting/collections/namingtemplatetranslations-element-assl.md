---
title: Elemento NamingTemplateTranslations (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- NamingTemplateTranslations Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- NamingTemplateTranslations
helpviewer_keywords:
- NamingTemplateTranslations element
ms.assetid: fde65778-1fa3-490a-9874-8bf2052ef25c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b1c7accfde72c3e64b3845f720c33fce5b55711e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48099408"
---
# <a name="namingtemplatetranslations-element-assl"></a>Elemento NamingTemplateTranslations (ASSL)
  Proporciona una colección de traducciones adaptadas para el elemento [NamingTemplate](../properties/namingtemplate-element-assl.md) del elemento primario, [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Attribute xsi:type="DimensionAttribute">  
   ...  
   <NamingTemplateTranslations>  
            <NamingTemplateTranslation xsi:type="Translation">...</NamingTemplateTranslation>  
...</NamingTemplateTranslations>  
   ...  
</Attribute>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Attribute](../objects/attribute-element-assl.md) de tipo [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)|  
|Elementos secundarios|[NamingTemplateTranslation](../objects/translation-element-assl.md) de tipo [Translation](translations-element-assl.md)|  
  
## <a name="remarks"></a>Comentarios  
 El valor de la `NamingTemplateTranslation` elemento es utilizado únicamente por los atributos primarios (en otras palabras, el valor de la [uso](../properties/usage-element-dimensionattribute-assl.md) elemento primario `DimensionAttribute` está establecido en *primario*.)  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.DimensionAttribute>.  
  
## <a name="see-also"></a>Vea también  
 [Colecciones &#40;ASSL&#41;](collections-assl.md)  
  
  
