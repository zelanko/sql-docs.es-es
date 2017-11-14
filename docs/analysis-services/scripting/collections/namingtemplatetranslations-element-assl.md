---
title: Elemento NamingTemplateTranslations (ASSL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/17/2017
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
apiname:
- NamingTemplateTranslations Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- NamingTemplateTranslations
helpviewer_keywords:
- NamingTemplateTranslations element
ms.assetid: fde65778-1fa3-490a-9874-8bf2052ef25c
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ed377512b4d2e27e6f3ec0d85066ac72b9996499
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="namingtemplatetranslations-element-assl"></a>Elemento NamingTemplateTranslations (ASSL)
  Proporciona una colección de traducciones adaptadas para el elemento [NamingTemplate](../../../analysis-services/scripting/properties/namingtemplate-element-assl.md) del elemento primario, [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md).  
  
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
|Tipo y longitud de los datos|Ninguno|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Attribute](../../../analysis-services/scripting/objects/attribute-element-assl.md) de tipo [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|Elementos secundarios|[NamingTemplateTranslation](../../../analysis-services/scripting/objects/namingtemplatetranslation-element-assl.md) de tipo [Translation](../../../analysis-services/scripting/objects/translation-element-assl.md)|  
  
## <a name="remarks"></a>Comentarios  
 El valor del elemento **NamingTemplateTranslation** es utilizado únicamente por los atributos primarios (es decir, el valor del elemento [Usage](../../../analysis-services/scripting/properties/usage-element-dimensionattribute-assl.md) del elemento primario **DimensionAttribute** se establece en *Parent*).  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.DimensionAttribute>.  
  
## <a name="see-also"></a>Vea también  
 [Colecciones de &#40; ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  

