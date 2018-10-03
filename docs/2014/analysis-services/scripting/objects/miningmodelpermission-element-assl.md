---
title: Elemento MiningModelPermission (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MiningModelPermission Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MiningModelPermission
helpviewer_keywords:
- MiningModelPermission element
ms.assetid: 4bd2f7e7-ff0d-404e-96fb-7e2c4eeb91e9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c6bad2b1bda46fcc1437a5f4c967ced8a6c726f0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48113475"
---
# <a name="miningmodelpermission-element-assl"></a>Elemento MiningModelPermission (ASSL)
  Define los miembros de los permisos de un [rol](role-element-assl.md) tiene elemento individual [MiningModel](miningmodel-element-assl.md) elemento.  
  
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
|Tipo y longitud de los datos|[Permiso](../data-type/permission-data-type-assl.md)|  
|Valor predeterminado|None|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[MiningModelPermissions](../collections/miningmodelpermissions-element-assl.md)|  
|Elementos secundarios|[AllowBrowsing](../properties/allowbrowsing-element-assl.md), [AllowDrillThrough](../properties/allowdrillthrough-element-assl.md)|  
  
## <a name="remarks"></a>Comentarios  
 En [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], puede habilitar la obtención de detalles en estructuras de minería de datos agregando el `AllowDrillthrough` permiso para el [MiningStructurePermissions](../collections/miningstructurepermissions-element-assl.md) colección. Si `AllowDrillthrough` está habilitada en la estructura de minería de datos y el modelo de minería de datos, cualquier miembro de un rol que tiene [elemento AllowDrillThrough &#40;ASSL&#41; ](../properties/allowdrillthrough-element-assl.md) permisos en el modelo pueden consultar el modelo de minería de datos y volver columnas de estructura que no se incluyeron en el modelo, mediante la sintaxis siguiente:  
  
```  
SELECT StructureColumn('<column name>') FROM <model>.CASES  
```  
  
 Por tanto, para proteger datos confidenciales o información personal, deberá conceder el permiso `AllowDrillthrough` en un modelo de minería de datos únicamente cuando sea necesario. Para obtener más información, consulte [elemento AllowDrillThrough &#40;ASSL&#41;](../properties/allowdrillthrough-element-assl.md).  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.MiningModelPermission>.  
  
## <a name="see-also"></a>Vea también  
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  
