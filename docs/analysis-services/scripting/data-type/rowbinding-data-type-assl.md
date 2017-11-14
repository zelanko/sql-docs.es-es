---
title: Tipo de datos RowBinding (ASSL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/03/2017
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
apiname:
- RowBinding Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- RowBinding
helpviewer_keywords:
- RowBinding data type
ms.assetid: 5a49a6e3-25f3-43c8-8529-bcf245b02415
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2900dc441d7ce296962faf1cd96bf823b597d35b
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="rowbinding-data-type-assl"></a>Tipo de datos RowBinding (ASSL)
  Define un tipo de datos derivado que representa un enlace a las filas de una tabla en una [DataSourceView](../../../analysis-services/scripting/objects/datasourceview-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<RowBinding>  
   <!-- The following elements extend Binding -->  
   <TableID>...</TableID>  
</RowBinding>  
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
|Elementos secundarios|[TableID](../../../analysis-services/scripting/properties/tableid-element-assl.md)|  
|Elementos derivados|Vea [enlace](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)|  
  
## <a name="remarks"></a>Comentarios  
 Para obtener más información sobre la **enlace** tipo, incluidas las tablas de objetos de Analysis Services Scripting Language (ASSL) de la **enlace** tipo y la jerarquía de herencia de **enlace**  tipos, consulte [enlazar el tipo de datos &#40; ASSL &#41; ](../../../analysis-services/scripting/data-type/binding-data-type-assl.md).  
  
 Para obtener información general de enlaces de datos en ASSL, vea [orígenes de datos y enlaces &#40; SSAS Multidimensional &#41; ](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.RowBinding>.  
  
## <a name="see-also"></a>Vea también  
 [Analysis Services Scripting Language tipos de datos XML &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  

