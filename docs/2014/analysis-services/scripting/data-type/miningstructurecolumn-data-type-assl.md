---
title: Tipo de datos MiningStructureColumn (ASSL) | Microsoft Docs
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
- MiningStructureColumn Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MiningStructureColumn
helpviewer_keywords:
- MiningStructureColumn data type
ms.assetid: b6d6e7a5-9c48-40c4-b147-8fcd5e429ae3
caps.latest.revision: 37
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0f30ccbc909db5197423c680e1e27b4ec55b97b0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37272081"
---
# <a name="miningstructurecolumn-data-type-assl"></a>Tipo de datos MiningStructureColumn (ASSL)
  Define un tipo de datos primitivo abstracto que representa información sobre una columna de un [MiningStructure](../objects/miningstructure-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<MiningStructureColumn>  
   <Name>...</Name>  
   <ID>...</ID>  
   <Description>...</Description>  
   <Type>...</Type>  
   <Annotations>...</Annotations>  
</MiningStructureColumn>  
```  
  
## <a name="data-type-characteristics"></a>Características del tipo de datos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipos de datos básicos|None|  
|Tipos de datos derivados|[ScalarMiningStructureColumn](miningstructurecolumn-data-type-assl.md), [TableMiningStructureColumn](tableminingstructurecolumn-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|None|  
|Elementos secundarios|[Las anotaciones](../collections/annotations-element-assl.md), [descripción](../properties/description-element-assl.md), [ID](../properties/id-element-assl.md), [nombre](../properties/name-element-assl.md), [tipo](../properties/type-element-miningstructurecolumn-assl.md)|  
|Elementos derivados|[Columna](../objects/column-element-assl.md) ([columnas](../collections/columns-element-assl.md) colección de [MiningStructure](../objects/miningstructure-element-assl.md))|  
  
## <a name="remarks"></a>Notas  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.MiningStructureColumn>.  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos XML de lenguaje Scripting de Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
