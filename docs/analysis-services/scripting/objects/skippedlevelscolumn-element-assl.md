---
title: Elemento SkippedLevelsColumn (ASSL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
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
apiname: SkippedLevelsColumn Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: SkippedLevelsColumn
helpviewer_keywords: SkippedLevelsColumn element
ms.assetid: 6b00a288-99c1-4735-9e6b-cd13ed4fa346
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: af0de4f281a6fd6734c8ecc456b4e80c20780a93
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="skippedlevelscolumn-element-assl"></a>Elemento SkippedLevelsColumn (ASSL)
    
> [!NOTE]  
>  Esta característica no se incluye en esta versión de Microsoft SQL Server. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan.  
  
 Proporciona los detalles de una columna que almacena el número de niveles omitidos (vacíos) entre cada miembro y su elemento primario.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<DimensionAttribute>  
   ...  
   <SkippedLevelsColumn xsi:type="DataItem">...</SkippedLevelsColumn>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|[Elemento de datos](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El **SkippedLevelsColumn** elemento solo es aplicable a los atributos primarios (en otras palabras, el valor de la [uso](../../../analysis-services/scripting/properties/usage-element-dimensionattribute-assl.md) (elemento) para la **DimensionAttribute** primario esté definida para *primario*). El elemento **SkippedLevelsColumn** contiene la columna o el atributo del atributo primario que almacena el número de niveles omitidos entre cada miembro y su miembro primario. Esto permite jerarquías de elementos primarios y secundarios que están basadas en el atributo primario para omitir niveles entre miembros. Los valores contenidos en esta columna o atributo deben ser enteros no negativos; de lo contrario, se produce un error de procesamiento. Si el elemento **SkippedLevelsColumn** no se especifica o no contiene ningún valor, el miembro actual tiene una profundidad de un nivel por debajo de su miembro primario.  
  
 Para obtener más información sobre la **DataItem** tipo, incluida una tabla de objetos de Analysis Services Scripting Language (ASSL) y las propiedades de la **DataItem** de tabla, vea [tipo de datos de elemento de datos &#40; ASSL &#41; ](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md).  
  
 El elemento que corresponde al elemento primario de **SkippedLevelsColumn** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.DimensionAttribute>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento Attributes &#40; ASSL &#41;](../../../analysis-services/scripting/collections/attributes-element-assl.md)   
 [Dimension, elemento &#40; ASSL &#41;](../../../analysis-services/scripting/objects/dimension-element-assl.md)   
 [Objetos de &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
