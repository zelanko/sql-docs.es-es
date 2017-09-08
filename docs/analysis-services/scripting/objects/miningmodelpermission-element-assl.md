---
title: Elemento MiningModelPermission (ASSL) | Documentos de Microsoft
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
- MiningModelPermission Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- MiningModelPermission
helpviewer_keywords:
- MiningModelPermission element
ms.assetid: 4bd2f7e7-ff0d-404e-96fb-7e2c4eeb91e9
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2cd366179355590dca84fb84f8a00e8dfc103a3f
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="miningmodelpermission-element-assl"></a>Elemento MiningModelPermission (ASSL)
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
 En [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], puede habilitar la obtención de detalles en estructuras de minería de datos mediante la adición de la **AllowDrillthrough** permiso para el [MiningStructurePermissions](../../../analysis-services/scripting/collections/miningstructurepermissions-element-assl.md) colección. Si **AllowDrillthrough** está habilitada en la estructura de minería de datos y el modelo de minería de datos, cualquier miembro de un rol que tiene [AllowDrillThrough, elemento &#40; ASSL &#41; ](../../../analysis-services/scripting/properties/allowdrillthrough-element-assl.md) permisos en el modelo pueden consultar el modelo de minería de datos y devolver columnas de estructura que no se incluyeron en el modelo, utilizando la sintaxis siguiente:  
  
```  
SELECT StructureColumn('<column name>') FROM <model>.CASES  
```  
  
 Por tanto, para proteger datos confidenciales o información personal, deberá conceder el permiso **AllowDrillthrough** en un modelo de minería de datos únicamente cuando sea necesario. Para obtener más información, vea [AllowDrillThrough, elemento &#40; ASSL &#41; ](../../../analysis-services/scripting/properties/allowdrillthrough-element-assl.md).  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.MiningModelPermission>.  
  
## <a name="see-also"></a>Vea también  
 [Objetos de &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
