---
title: Elemento AllowedRowsExpression (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: ec24b11d-d11e-4369-a619-7e41a3c46159
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a23acca8488d5fa747d29338240cf98e0f703ecc
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48057255"
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
|Tipo y longitud de los datos|String|  
|Valor predeterminado|None|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[CellPermission](../objects/cellpermission-element-assl.md), [StandardAction](../data-type/action-data-type-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 Para el `CellPermission` elemento, el `Expression` elemento contiene una expresión MDX lógica que identifica las celdas aplicables a los derechos indicados por el [acceso](access-element-assl.md) elemento de la `CellPermission` elemento. Si el valor de un elemento `Expression` para un elemento `CellPermission` está vacío, se omite el elemento `CellPermission`.  
  
 Para el elemento `StandardAction`, el elemento `Expression` contiene una expresión MDX que representa el contenido de la acción. Si el valor de un elemento `Expression` para un elemento `StandardAction` está vacío, se omite el elemento `StandardAction`.  
  
 Los elementos que corresponden a los elementos primarios en el modelo de objetos Objetos de administración de análisis (AMO) son <xref:Microsoft.AnalysisServices.CellPermission> y <xref:Microsoft.AnalysisServices.StandardAction>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
