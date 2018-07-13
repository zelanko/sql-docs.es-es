---
title: Tipo de datos ScalarMiningStructureColumn (ASSL) | Microsoft Docs
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
- ScalarMiningStructureColumn Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ScalarMiningStructureColumn
helpviewer_keywords:
- ScalarMiningStructureColumn data type
ms.assetid: 8f4afc15-601c-4189-bc45-f5a216aed879
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 90f855bf55292b310e32a167dc005ab2f2f81c14
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37211695"
---
# <a name="scalarminingstructurecolumn-data-type-assl"></a>Tipo de datos ScalarMiningStructureColumn (ASSL)
  Define un tipo de datos derivado que representa un [MiningStructureColumn](miningstructurecolumn-data-type-assl.md) elemento que contiene valores escalares, en lugar de las tablas anidadas asociadas con el [TableMiningStructureColumn](tableminingstructurecolumn-data-type-assl.md) elemento que contiene tablas anidadas.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<ScalarMiningStructureColumn>  
   <!-- The following elements extend MiningStructureColumn -->  
   <IsKey>...</IsKey>  
   <Source>...</Source>  
   <Distribution>...</Distribution>  
   <ModelingFlags>...</ModelingFlags>  
   <Content>...</Content>  
   <ClassifiedColumnID>...</<ClassifiedColumnI  
   <DiscretizationMethod>...</DiscretizationMethod>  
   <DiscretizationBucketCount>...</DiscretizationBucketCount>  
   <KeyColumns>...</KeyColumns>  
   <NameColumn>...</NameColumn>  
   <Translations>...</Translations>  
</ScalarMiningStructureColumn>  
```  
  
## <a name="data-type-characteristics"></a>Características del tipo de datos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipos de datos base|[MiningStructureColumn](miningstructurecolumn-data-type-assl.md)|  
|Tipos de datos derivados|None|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|None|  
|Elementos secundarios|[ClassifiedColumnID](../properties/id-element-assl.md), [contenido](../properties/content-element-assl.md), [DiscretizationBucketCount](../properties/discretizationbucketcount-element-assl.md), [DiscretizationMethod](../properties/discretizationmethod-element-assl.md), [distribución](../properties/distribution-element-assl.md), [IsKey](../properties/iskey-element-assl.md), [KeyColumns](../collections/columns-element-assl.md), [ModelingFlags](../collections/modelingflags-element-assl.md), [NameColumn](../objects/column-element-assl.md), [origen](../properties/source-element-binding-assl.md), [ Traducciones](../collections/translations-element-assl.md)|  
|Elementos derivados|[Columna](../objects/column-element-assl.md) ([columnas](../collections/columns-element-assl.md) colección de [MiningStructure](../objects/miningstructure-element-assl.md))|  
  
## <a name="remarks"></a>Notas  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>.  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos XML de lenguaje Scripting de Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
