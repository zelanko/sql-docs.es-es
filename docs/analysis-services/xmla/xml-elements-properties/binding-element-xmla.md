---
title: Elemento Binding (XMLA) | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c51e99c4dcfde8de6060bf57e248d32322da8ac9
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34574077"
---
# <a name="binding-element-xmla"></a>Elemento Binding (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Define un enlace fuera de línea para un objeto de Analysis Services, como un atributo en una dimensión para el [enlaces](../../../analysis-services/xmla/xml-elements-properties/bindings-element-xmla.md) colección de un [lote](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md) o [proceso](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md) comando.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Bindings>  
   <Binding xsi:type="DimensionAttributeBinding">...</Binding>  
   <!-- or -->  
   <Binding xsi:type="MeasureGroupAttributeBinding">...</Binding>  
   <!-- or -->  
   <Binding xsi:type="PartitionBinding">...</Binding>  
</Bindings>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|[DimensionAttributeBinding](../../../analysis-services/scripting/data-type/dimensionattributebinding-data-type-out-of-line-assl.md), [MeasureGroupAttributeBinding](../../../analysis-services/scripting/data-type/measuregroupattributebinding-data-type-out-of-line-assl.md), [PartitionBinding](../../../analysis-services/scripting/data-type/partitionbinding-data-type-assl.md)|  
|Valor predeterminado|None|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Enlaces](../../../analysis-services/xmla/xml-elements-properties/bindings-element-xmla.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 **Enlace** elementos definen enlaces fuera de línea, que no sea de orígenes de datos y vistas del origen de datos, para [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] objetos para ser procesados por un **lote** o **proceso** comando. Para obtener más información acerca de los objetos de procesamiento, vea [Processing Objects &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/processing-objects-xmla.md).  
  
 Para obtener más información acerca de los enlaces fuera de línea, consulte [orígenes de datos y enlaces &#40;SSAS multidimensionales&#41;](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
## <a name="see-also"></a>Vea también
 [Propiedades &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
