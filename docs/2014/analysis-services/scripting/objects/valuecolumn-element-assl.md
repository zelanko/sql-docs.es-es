---
title: Elemento ValueColumn (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ValueColumn Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- ValueColumn element
ms.assetid: 6c2d6822-8ecc-46df-9fa9-bb92ac716c36
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 876d5efb4d4b84e8f42cfd3c360258c8cb67d865
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48048146"
---
# <a name="valuecolumn-element-assl"></a>Elemento ValueColumn (ASSL)
  Identifica la columna que proporciona el valor del elemento primario.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<DimensionAttribute>  
   ...  
   <ValueColumn xsi:type="DataItem">...</ValueColumn>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|[DataItem](../data-type/dataitem-data-type-assl.md)|  
|Valor predeterminado|Varía (ver Notas)|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 Si el [NameColumn](namecolumn-element-assl.md) elemento de `DimensionAttribute` se especifica, el mismo `DataItem` valores se utilizan como valores predeterminados para el `ValueColumn` elemento. Si el `NameColumn` elemento de `DimensionAttribute` no se especifica y el [KeyColumns](../collections/keycolumns-element-assl.md) colección de `DimensionAttribute` contiene un único [KeyColumn](keycolumn-element-assl.md) elemento representa una columna de clave con una cadena tipo de datos, los mismos `DataItem` valores se utilizan como valores predeterminados para el `ValueColumn` elemento.  
  
 Para obtener más información sobre la `DataItem` tipo, incluida una tabla de objetos de Analysis Services Scripting Language (ASSL) y las propiedades de la `DataItem` , vea [tipo de datos DataItem &#40;ASSL&#41;](../data-type/dataitem-data-type-assl.md).  
  
 Los elementos que corresponden a los elementos primarios de `NameColumn` en el modelo de objetos de Analysis Management Objects (AMO) son <xref:Microsoft.AnalysisServices.DimensionAttribute> y <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>.  
  
## <a name="see-also"></a>Vea también  
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  
