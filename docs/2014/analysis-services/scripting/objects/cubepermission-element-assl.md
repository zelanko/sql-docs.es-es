---
title: Elemento CubePermission (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- CubePermission Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CubePermission
helpviewer_keywords:
- CubePermission element
ms.assetid: b144b623-ff20-4ead-91ad-4c718f3b140b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7dc2c8cc50ccf61515241c7b9861c438ae369022
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48055132"
---
# <a name="cubepermission-element-assl"></a>Elemento CubePermission (ASSL)
  Define los permisos de los miembros de un determinado [rol](role-element-assl.md) elemento en un determinado [cubo](cube-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<CubePermissions>  
   <CubePermission>  
      <!-- The following elements extend Permission -->  
      <ReadSourceData>...</ReadSourceData>  
            <DimensionPermissions>...</DimensionPermissions>  
            <CellPermissions>...</CellPermissions>  
   </CubePermission>  
</CubePermissions>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|[Permiso](../data-type/permission-data-type-assl.md)|  
|Valor predeterminado|None|  
|Cardinalidad|0-n: Elemento opcional que puede aparecer una vez o más.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[CubePermissions](../collections/cubepermissions-element-assl.md)|  
|Elementos secundarios|[CellPermissions](../collections/cellpermissions-element-assl.md), [DimensionPermissions](../collections/dimensionpermissions-element-assl.md), [ReadSourceData](data-element-assl.md)|  
  
## <a name="remarks"></a>Comentarios  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.CubePermission>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento de cubo &#40;ASSL&#41;](cube-element-assl.md)   
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  
