---
title: Tipo de datos Hierarchy (ASSL) | Microsoft Docs
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
- Hierarchy Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- Hierarchy data type
ms.assetid: 2e05917e-7e5d-4dd1-817b-4ff5647747ff
caps.latest.revision: 17
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b20bed156e97c33a1c9f9df02677ef403767e472
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37230015"
---
# <a name="hierarchy-data-type-assl"></a>Tipo de datos Hierarchy (ASSL)
  Define un tipo de datos primitivo que representa una jerarquía en una dimensión.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Hierarchy>  
   <Name>...</Name>  
   <ID>...</ID>  
   <Description>...</Description>  
   <DisplayFolder>...</DisplayFolder>  
   <Translations>...</Translations>  
   <AllMemberName>...</AllMemberName>  
   <AllMemberTranslations>...</AllMemberTranslation>  
   <MemberNamesUnique>...</MemberNamesUnique>  
   <AllowDuplicateNames>...</AllowDuplicateNames>  
   <Levels>...</Levels>  
   <Annotations>...</Annotation>  
</Hierarchy>  
```  
  
## <a name="data-type-characteristics"></a>Características del tipo de datos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipos de datos básicos|None|  
|Tipos de datos derivados|None|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|None|  
|Elementos secundarios|[AllMemberName](../properties/name-element-assl.md), [AllMemberTranslations](../collections/translations-element-assl.md), [AllowDuplicateNames](../properties/allowduplicatenames-element-assl.md), [anotaciones](../collections/annotations-element-assl.md), [descripción](../properties/description-element-assl.md), [ DisplayFolder](../properties/displayfolder-element-assl.md), [ID](../properties/id-element-assl.md), [niveles](../collections/levels-element-assl.md), [MemberNamesUnique](../properties/membernamesunique-element-assl.md), [nombre](../properties/name-element-assl.md), [ Traducciones](../collections/translations-element-assl.md)|  
|Elementos derivados|[Hierarchy](../objects/hierarchy-element-assl.md)|  
  
## <a name="remarks"></a>Notas  
 El elemento *MemberNamesUnique* no se admite en DevelopmentMode 1 o 2 para los modos de servidor SharePoint o tabular, respectivamente.  
  
 El elemento *MemberKeysUnique* no se admite en DevelopmentMode 1 o 2 para los modos de servidor SharePoint o tabular, respectivamente.  
  
 El elemento *AllowDuplicateNames* no se admite en DevelopmentMode 1 o 2 para los modos de servidor SharePoint o tabular, respectivamente.  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.Hierarchy>.  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos XML de lenguaje Scripting de Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
