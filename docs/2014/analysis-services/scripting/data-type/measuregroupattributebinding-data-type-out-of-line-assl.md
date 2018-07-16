---
title: Tipo de datos MeasureGroupAttributeBinding (fuera de línea) (ASSL) | Microsoft Docs
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
- MeasureGroupAttributeBinding Data Type (out-of-line)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- MeasureGroupAttributeBinding data type
ms.assetid: bfe09a95-4e04-4f93-9389-7dd0b4c8f5e4
caps.latest.revision: 8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 244656b0ae951ec5f8274f11e58153faef80957d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37218215"
---
# <a name="measuregroupattributebinding-data-type-out-of-line-assl"></a>Tipo de datos MeasureGroupAttributeBinding (fuera de línea) (ASSL)
  Define un tipo de datos derivado que representa un enlace fuera de línea para un atributo de una dimensión incluida en un grupo de medida.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<MeasureGroupAttributeBinding>  
   <!-- The following elements extend Binding -->  
   <DatabaseID>...</DatabaseID>  
   <CubeID>...</CubeID>  
   <MeasureGroupID>...</MeasureGroupID>  
   <GranularityAttributeID>...</GranularityAttributeID>  
   <Source>...</Source>  
</MeasureGroupAttributeBinding>  
```  
  
## <a name="data-type-characteristics"></a>Características del tipo de datos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipos de datos base|[Enlace](binding-data-type-assl.md)|  
|Tipos de datos derivados|None|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|None|  
|Elementos secundarios|[CubeID](../properties/id-element-assl.md), [DatabaseID](../../xmla/xml-elements-properties/id-element-xmla.md), [MeasureGroupID](../properties/measuregroupid-element-assl.md), [GranularityAttributeID](../properties/attributeid-element-assl.md), [origen](../properties/source-element-binding-assl.md)|  
|Elementos derivados|[Enlace](../../xmla/xml-elements-properties/binding-element-xmla.md) ([enlaces](../collections/attributes-element-assl.md) colección de XML for Analysis (XMLA) [Batch](../../xmla/xml-elements-commands/batch-element-xmla.md) y [proceso](../../xmla/xml-elements-commands/process-element-xmla.md) comandos)|  
  
## <a name="remarks"></a>Notas  
 Para obtener más información sobre los enlaces fuera de línea, consulte [orígenes de datos y enlaces &#40;Multidimensional de SSAS&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos XML de lenguaje Scripting de Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
