---
title: Elemento CellPermission (ASSL) | Documentos de Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9c4b6c9420be8eec3ba6d856f7c6312bfeb9b7f9
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="cellpermission-element-assl"></a>Elemento CellPermission (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Se describen los permisos que los miembros de un [rol](../../../analysis-services/scripting/objects/role-element-assl.md) elemento tienen en celdas individuales dentro de un [cubo](../../../analysis-services/scripting/objects/cube-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<CellPermissions>  
   <CellPermission>  
      <Access>...</Access>  
            <Description>...</Description>  
      <Expression>...</Expression>  
      <Annotations>...</Annotations>  
   </CellPermission>  
</CellPermissions>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Ninguno|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[CellPermissions](../../../analysis-services/scripting/collections/cellpermissions-element-assl.md)|  
|Elementos secundarios|[Acceso](../../../analysis-services/scripting/properties/access-element-assl.md), [anotaciones](../../../analysis-services/scripting/collections/annotations-element-assl.md), [descripción](../../../analysis-services/scripting/properties/description-element-assl.md), [expresión](../../../analysis-services/scripting/properties/expression-element-assl.md)|  
  
## <a name="remarks"></a>Comentarios  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.CellPermission>.  
  
## <a name="see-also"></a>Vea también  
 [Objetos de & #40; ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
