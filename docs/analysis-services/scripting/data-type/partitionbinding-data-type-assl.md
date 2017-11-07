---
title: Tipo de datos PartitionBinding (ASSL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- PartitionBinding Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- PartitionBinding
helpviewer_keywords:
- PartitionBinding data type
ms.assetid: 859d4b47-31c7-4678-9388-254fec484299
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 83a65b2fb8c00490d0ff3a4feda0d4a6854aef6d
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="partitionbinding-data-type-assl"></a>Tipo de datos PartitionBinding (ASSL)
  Define un tipo de datos derivado que representa un enlace a un [partición](../../../analysis-services/scripting/objects/partition-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<PartitionBinding>  
   <DatabaseID>...</DatabaseID>  
   <CubeID>...</CubeID>  
   <PartitionID>...</PartitionID>  
   <Source>...</Source>  
</PartitionBinding>  
```  
  
## <a name="data-type-characteristics"></a>Características del tipo de datos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipos de datos base|[Enlace](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)|  
|Tipos de datos derivados|Ninguno|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|Ninguno|  
|Elementos secundarios|[CubeID](../../../analysis-services/xmla/xml-elements-properties/cubeid-element-xmla.md), [DatabaseID](../../../analysis-services/xmla/xml-elements-properties/databaseid-element-xmla.md), [PartitionID](../../../analysis-services/xmla/xml-elements-properties/partitionid-element-xmla.md), [origen](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|  
|Elementos derivados|Vea [enlace](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)|  
  
## <a name="remarks"></a>Comentarios  
 Para obtener información adicional sobre la **enlace** tipo, incluidas las tablas de objetos de Analysis Services Scripting Language (ASSL) de la **enlace** tipo y la jerarquía de herencia de  **Enlace** tipos, consulte [enlazar el tipo de datos &#40; ASSL &#41; ](../../../analysis-services/scripting/data-type/binding-data-type-assl.md).  
  
 Para obtener información general de enlaces de datos en ASSL, vea [orígenes de datos y enlaces &#40; SSAS Multidimensional &#41; ](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
## <a name="see-also"></a>Vea también  
 [Analysis Services Scripting Language tipos de datos XML &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  

