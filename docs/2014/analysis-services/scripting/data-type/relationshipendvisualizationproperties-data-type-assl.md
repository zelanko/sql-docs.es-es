---
title: Tipo de datos RelationshipEndVisualizationProperties (ASSL) | Documentos de Microsoft
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
ms.assetid: 11f9a10f-d36c-4faf-b595-3fe969d1935e
caps.latest.revision: 5
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 13bde90af2ecbb8aba03bea4d140139c8437a747
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199761"
---
# <a name="relationshipendvisualizationproperties-data-type-assl"></a>Tipo de datos RelationshipEndVisualizationProperties (ASSL)
  Define un tipo de datos primitivo que representa un extremo de la relación en una relación.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<RelationshipEnd>  
   <FolderPosition>...</FolderPosition>  
   <ContextualNameRule>...</ContextualNameRule>  
   <DefaultDetailsPosition>...</DefaultDetailsPosition>  
   <DisplayKeyPosition>...</DisplayKeyPosition>  
   <CommonIdentifierPosition>...</CommonIdentifierPosition>  
   <IsDefaultMeasure>...</IsDefaultMeasure>  
   <IsDefaultImage>...</IsDefaultImage>  
   <SortPropertiesPosition>...</SortPropertiesPosition>  
</RelationshipEnd>  
```  
  
## <a name="data-type-characteristics"></a>Características del tipo de datos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipos de datos básicos|None|  
|Tipos de datos derivados|None|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[RelationshipEnd](relationshipend-data-type-assl.md)|  
|Elementos secundarios|[FolderPosition](../../xmla/xml-elements-properties/folderposition-element-xml.md), [ContextualNameRule](../../xmla/xml-elements-properties/contextualnamerule-element-xml.md), [DefaultDetailsPosition](../../xmla/xml-elements-properties/defaultdetailsposition-element-xml.md), [DisplayKeyPosition](../../xmla/xml-elements-properties/displaykeyposition-element-xml.md), [CommonIdentifierPosition](../../xmla/xml-elements-properties/commonidentifierposition-element-xml.md), [IsDefaultMeasure](../../xmla/xml-elements-properties/isdefaultmeasure-element-xml.md), [IsDefaultImage](../../xmla/xml-elements-properties/isdefaultimage-element-xml.md), [SortPropertiesPosition](../../xmla/xml-elements-properties/sortpropertiesposition-element-xml.md)|  
|Elementos derivados||  
  
## <a name="remarks"></a>Notas  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.RelationshipEnd>.  
  
  