---
title: Tipo de datos AttributeBinding (ASSL) | Documentos de Microsoft
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
- AttributeBinding Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- AttributeBinding
helpviewer_keywords:
- AttributeBinding data type
ms.assetid: 24d511a9-d0eb-4150-9f78-541e03963d67
caps.latest.revision: 44
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1c26f2de824dc8fb2b0a620afce386b0cefd53b9
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="attributebinding-data-type-assl"></a>Tipo de datos AttributeBinding (ASSL)
  Define un tipo de datos derivado que representa un enlace para un [atributo](../../../analysis-services/scripting/objects/attribute-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<AttributeBinding>  
   <AttributeID>...</AttributeID>  
      <Type>...</Type>  
   <Ordinal>...</Ordinal>  
</AttributeBinding>  
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
|Elementos secundarios|[AttributeID](../../../analysis-services/scripting/properties/attributeid-element-assl.md), [Ordinal](../../../analysis-services/scripting/properties/ordinal-element-assl.md), [tipo](../../../analysis-services/scripting/properties/type-element-binding-assl.md)|  
|Elementos derivados|Vea [enlace](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)|  
  
## <a name="remarks"></a>Comentarios  
 Para obtener información adicional sobre la **enlace** tipo de datos, incluidas las tablas de objetos de Analysis Services Scripting Language (ASSL) derivados de la **enlace** tipo de datos, vea [el enlace de datos Tipo de &#40; ASSL &#41; ](../../../analysis-services/scripting/data-type/binding-data-type-assl.md).  
  
 Para obtener información general de enlaces de datos en ASSL, vea [orígenes de datos y enlaces &#40; SSAS Multidimensional &#41; ](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.AttributeBinding>.  
  
## <a name="see-also"></a>Vea también  
 [Analysis Services Scripting Language tipos de datos XML &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  

