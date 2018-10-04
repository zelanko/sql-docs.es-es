---
title: Elemento MiningModelPermissions (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MiningModelPermissions Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MiningModelPermissions
helpviewer_keywords:
- MiningModelPermissions element
ms.assetid: 6cbcf029-9627-4839-9fc5-15e58e1ba0c3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 214e3286d9e12aed8ffa571442cfec4184495a78
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48173885"
---
# <a name="miningmodelpermissions-element-assl"></a>Elemento MiningModelPermissions (ASSL)
  Contiene la colección de permisos para un [MiningModel](../objects/miningmodel-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<MiningModel>  
   ...  
   <MiningModelPermissions>  
      <MiningModelPermission xsi:type="Permission">...</MiningModelPermission>  
   </MiningModelPermissions>  
   ...  
</MiningModel>  
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
|Elementos primarios|[MiningModel](../objects/miningmodel-element-assl.md)|  
|Elementos secundarios|[MiningModelPermission](../objects/miningmodelpermission-element-assl.md) typu [permiso](../data-type/permission-data-type-assl.md)|  
  
## <a name="remarks"></a>Comentarios  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.MiningModelPermissionCollection>.  
  
## <a name="see-also"></a>Vea también  
 [Tipo de datos Permission &#40;ASSL&#41;](../data-type/permission-data-type-assl.md)   
 [Colecciones &#40;ASSL&#41;](collections-assl.md)  
  
  
