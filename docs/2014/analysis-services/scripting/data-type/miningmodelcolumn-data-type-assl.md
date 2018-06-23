---
title: Tipo de datos MiningModelColumn (ASSL) | Documentos de Microsoft
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
- MiningModelColumn Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MiningModelColumn
helpviewer_keywords:
- MiningModelColumn data type
ms.assetid: de8bf815-43b4-4983-bdb9-b67e8563be0e
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 6943acb9e15e1133da5aba8c49e0a14f3c61377c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36111233"
---
# <a name="miningmodelcolumn-data-type-assl"></a>Tipo de datos MiningModelColumn (ASSL)
  Define un tipo de datos primitivo que representa información sobre una columna de un [MiningModel](../objects/miningmodel-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<MiningModelColumn>  
      <Name>...</Name>  
      <ID>...</ID>  
      <Description>...</<Description>  
      <SourceColumnID>...</SourceColumnID>  
            <Usage>...</Usage>  
            <Translations>...</Translations>  
      <Columns>...</Columns>  
      <ModelingFlags>...</ModelingFlags>  
      <Annotations>...</Annotations>  
</MiningModelColumn>  
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
|Elementos secundarios|[Anotaciones](../collections/annotations-element-assl.md), [columnas](../collections/columns-element-assl.md), [descripción](../properties/description-element-assl.md), [identificador](../properties/id-element-assl.md), [ModelingFlags](../collections/modelingflags-element-assl.md), [nombre](../properties/name-element-assl.md) , [SourceColumnID](../properties/sourcecolumnid-element-assl.md), [traducciones](../collections/translations-element-assl.md), [uso](../properties/usage-element-dimensionattribute-assl.md)|  
|Elementos derivados|[Columna](../objects/column-element-assl.md) ([columnas](../collections/columns-element-assl.md), colección de [MiningModel](../objects/miningmodel-element-assl.md))|  
  
## <a name="remarks"></a>Notas  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.MiningModelColumn>.  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos XML de lenguaje Scripting de Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  