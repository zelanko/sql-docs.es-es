---
title: Elemento NameColumn (ASSL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/15/2017
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
apiname: NameColumn Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: NameColumn
helpviewer_keywords: NameColumn element
ms.assetid: 9ff79f2e-26d7-4ab9-a166-14c2c2d1fc07
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 513b6954b19130dfe67ffdb960f3d63dbe552dbb
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="namecolumn-element-assl"></a>Elemento NameColumn (ASSL)
  Identifica la columna que proporciona el nombre del elemento primario.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<DimensionAttribute> <!-- or ScalarMiningStructureColumn -->  
   ...  
   <NameColumn xsi:type="DataItem">...</NameColumn>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|[Elemento de datos](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|  
|Valor predeterminado|Vea la siguiente tabla.|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
|Antecesor o elemento primario|Valor predeterminado|  
|------------------------|-------------------|  
|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|Varía (ver Notas)|  
|[ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|Ninguno|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md), [ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 Si el [KeyColumns](../../../analysis-services/scripting/collections/keycolumns-element-assl.md) colección de **DimensionAttribute** contiene un único [KeyColumn](../../../analysis-services/scripting/objects/keycolumn-element-assl.md) elemento que representa una columna de clave con un tipo de datos de cadena, los mismos **DataItem** valores se utilizan como valores predeterminados para la **NameColumn** elemento.  
  
 Para obtener más información sobre la **DataItem** tipo, incluida una tabla de objetos de Analysis Services Scripting Language (ASSL) y las propiedades de la **DataItem** los tipos, vea [tipo de datos de elemento de datos &#40; ASSL &#41; ](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md).  
  
 Los elementos que corresponden a los elementos primarios de **NameColumn** en el modelo de objetos de Analysis Management Objects (AMO) son <xref:Microsoft.AnalysisServices.DimensionAttribute> y <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>.  
  
## <a name="see-also"></a>Vea también  
 [Objetos de &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
