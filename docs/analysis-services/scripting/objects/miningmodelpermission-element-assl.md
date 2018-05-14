---
title: Elemento MiningModelPermission (ASSL) | Documentos de Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6f05a12d5be30826e5a826320f2eb5a6c604456e
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="miningmodelpermission-element-assl"></a>Elemento MiningModelPermission (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Define los miembros de los permisos de un [rol](../../../analysis-services/scripting/objects/role-element-assl.md) elemento tiene en un individuo [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<MiningModelPermissions>  
   <MiningModelPermission xsi:type="Permission">  
      <!-- The following elements extend Permission -->  
      <AllowDrillThrough>...</AllowDrillThrough>  
      <AllowBrowsing>...</AllowBrowsing>  
   </MiningModelPermission>  
</MiningModelPermissions>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|[Permiso](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[MiningModelPermissions](../../../analysis-services/scripting/collections/miningmodelpermissions-element-assl.md)|  
|Elementos secundarios|[AllowBrowsing](../../../analysis-services/scripting/properties/allowbrowsing-element-assl.md), [AllowDrillThrough](../../../analysis-services/scripting/properties/allowdrillthrough-element-assl.md)|  
  
## <a name="remarks"></a>Comentarios  
 En [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], puede habilitar la obtención de detalles en estructuras de minería de datos mediante la adición de la **AllowDrillthrough** permiso para el [MiningStructurePermissions](../../../analysis-services/scripting/collections/miningstructurepermissions-element-assl.md) colección. Si **AllowDrillthrough** está habilitada en la estructura de minería de datos y el modelo de minería de datos, cualquier miembro de un rol que tiene [elemento AllowDrillThrough &#40;ASSL&#41; ](../../../analysis-services/scripting/properties/allowdrillthrough-element-assl.md) pueden consultar los permisos en el modelo el modelo de minería de datos y columnas de estructura de valor devuelto que no se incluyeron en el modelo, utilizando la sintaxis siguiente:  
  
```  
SELECT StructureColumn('<column name>') FROM <model>.CASES  
```  
  
 Por tanto, para proteger datos confidenciales o información personal, deberá conceder el permiso **AllowDrillthrough** en un modelo de minería de datos únicamente cuando sea necesario. Para obtener más información, consulte [elemento AllowDrillThrough &#40;ASSL&#41;](../../../analysis-services/scripting/properties/allowdrillthrough-element-assl.md).  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.MiningModelPermission>.  
  
## <a name="see-also"></a>Vea también  
 [Objetos de & #40; ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
