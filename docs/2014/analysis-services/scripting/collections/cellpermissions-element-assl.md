---
title: Elemento CellPermissions (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- CellPermissions Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CellPermissions
helpviewer_keywords:
- CellPermissions element
ms.assetid: 4a604f2f-f4c3-42bd-a42b-951263942cc6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f1a700960586c9cb6e26475ffb0b6b9a52f9939b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48133595"
---
# <a name="cellpermissions-element-assl"></a>Elemento CellPermissions (ASSL)
  Contiene la colección de permisos para las celdas en el asociado [cubo](../objects/cube-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<CubePermission>  
   ...  
   <CellPermissions>  
      <CellPermission>...</CellPermission>  
   </CellPermissions>  
   ...  
</CubePermission>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Elemento CubePermission](../objects/cubepermission-element-assl.md)|  
|Elementos secundarios|[CellPermission](../objects/cellpermission-element-assl.md)|  
  
## <a name="remarks"></a>Comentarios  
 La colección puede contener hasta un `CellPermission` cada valor permitido del objeto la [acceso](../properties/access-element-assl.md) elemento.  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.CellPermissionCollection>.  
  
## <a name="see-also"></a>Vea también  
 [Tipo de datos Permission &#40;ASSL&#41;](../data-type/permission-data-type-assl.md)   
 [Colecciones &#40;ASSL&#41;](collections-assl.md)  
  
  
