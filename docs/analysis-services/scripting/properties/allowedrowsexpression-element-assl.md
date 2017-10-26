---
title: Elemento AllowedRowsExpression (ASSL) | Documentos de Microsoft
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
applies_to:
- SQL Server 2016 Preview
ms.assetid: ec24b11d-d11e-4369-a619-7e41a3c46159
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: cf9c12f586ff7ffab5f627f049748d1f44eb9428
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="allowedrowsexpression-element-assl"></a>Elemento AllowedRowsExpression (ASSL)
  Contiene una expresión de análisis de datos (DAX), de tipo booleano, que define el contenido del elemento primario.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<CellPermission> <!-- or StandardAction -->  
   ...  
   <Expression>...</Expression>  
   ...  
</CellPermission>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Cadena|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[CellPermission](../../../analysis-services/scripting/objects/cellpermission-element-assl.md), [StandardAction](../../../analysis-services/scripting/data-type/standardaction-data-type-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 Para el **CellPermission** elemento, el **expresión** elemento contiene una expresión MDX lógica que identifica las celdas aplicables a los derechos indicados por el [acceso](../../../analysis-services/scripting/properties/access-element-assl.md) elemento de la **CellPermission** elemento. Si el valor de un **expresión** (elemento) para un **CellPermission** elemento está vacío, el **CellPermission** elemento se omite.  
  
 Para el **StandardAction** elemento, el **expresión** elemento contiene una expresión MDX que representa el contenido de la acción. Si el valor de un **expresión** (elemento) para un **StandardAction** elemento está vacío, el **StandardAction** elemento se omite.  
  
 Los elementos que corresponden a los elementos primarios en el modelo de objetos Objetos de administración de análisis (AMO) son <xref:Microsoft.AnalysisServices.CellPermission> y <xref:Microsoft.AnalysisServices.StandardAction>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

