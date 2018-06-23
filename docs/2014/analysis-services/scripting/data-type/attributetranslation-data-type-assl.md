---
title: Tipo de datos AttributeTranslation (ASSL) | Documentos de Microsoft
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
- AttributeTranslation Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AttributeTranslation
helpviewer_keywords:
- AttributeTranslation data type
ms.assetid: a0e29941-ef08-42ad-ab9c-b2efd7910895
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 9e7f5fe2157b407cae3909666329537f85a8b7e9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36108193"
---
# <a name="attributetranslation-data-type-assl"></a>Tipo de datos AttributeTranslation (ASSL)
  Define un tipo de datos derivado que representa una traducción asociada con una [atributo](../objects/attribute-element-assl.md) elemento  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<AttributeTranslation>  
   <!-- The following elements extend Translation -->  
   <CaptionColumn>...</CaptionColumn>  
   <MembersWithDataCaption>...</MembersWithDataCaption>  
</AttributeTranslation>  
```  
  
## <a name="data-type-characteristics"></a>Características del tipo de datos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipos de datos base|[Traducción](translation-data-type-assl.md)|  
|Tipos de datos derivados|None|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|None|  
|Elementos secundarios|[CaptionColumn](../objects/column-element-assl.md), [MembersWithDataCaption](../properties/caption-element-assl.md)|  
|Elementos derivados|Vea [traducción](../objects/translation-element-assl.md) ([traducciones](../collections/translations-element-assl.md) colección de [DimensionAttribute](dimensionattribute-data-type-assl.md) o [ScalarMiningStructureColumn](miningstructurecolumn-data-type-assl.md))|  
  
## <a name="remarks"></a>Notas  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.AttributeTranslation>.  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos XML de lenguaje Scripting de Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  