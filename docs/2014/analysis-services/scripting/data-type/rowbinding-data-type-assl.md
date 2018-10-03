---
title: Tipo de datos RowBinding (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- RowBinding Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- RowBinding
helpviewer_keywords:
- RowBinding data type
ms.assetid: 5a49a6e3-25f3-43c8-8529-bcf245b02415
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9fb15b72b3031b62136f65b175cb0ded8c3297a9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48203225"
---
# <a name="rowbinding-data-type-assl"></a>Tipo de datos RowBinding (ASSL)
  Define un tipo de datos derivado que representa un enlace a las filas de una tabla en un [DataSourceView](../objects/datasourceview-element-assl.md) elemento.  
  
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
|Tipos de datos base|[enlace](binding-data-type-assl.md)|  
|Tipos de datos derivados|None|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|None|  
|Elementos secundarios|[TableID](../properties/id-element-assl.md)|  
|Elementos derivados|Consulte [enlace](binding-data-type-assl.md)|  
  
## <a name="remarks"></a>Comentarios  
 Para obtener más información sobre la `Binding` tipo, incluidas las tablas de objetos de Analysis Services Scripting Language (ASSL) de la `Binding` tipo y la jerarquía de herencia de `Binding` tipos, vea [tipo de enlace de datos &#40;ASSL &#41;](binding-data-type-assl.md).  
  
 Para obtener información general de los enlaces de datos en ASSL, vea [orígenes de datos y enlaces &#40;Multidimensional de SSAS&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.RowBinding>.  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos XML de lenguaje Scripting de Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
