---
title: Elemento AllowedRowsExpression (ASSL) | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7bca46eeaafa4f0e028b08d9f70903f1e6e84b9f
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="allowedrowsexpression-element-assl"></a>Elemento AllowedRowsExpression (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
 [Propiedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
