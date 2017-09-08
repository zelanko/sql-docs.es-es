---
title: Dimensionpermission, elemento (ASSL) | Documentos de Microsoft
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
- DimensionPermission Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- DimensionPermission
helpviewer_keywords:
- DimensionPermission element
ms.assetid: e06efbda-64fd-4dca-a2b5-c8ffbf21512c
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 77b4db8b956272d881823308729480fad9719546
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="dimensionpermission-element-assl"></a>Dimensionpermission, elemento (ASSL)
  Define los permisos que pertenecen a un determinado [rol](../../../analysis-services/scripting/objects/role-element-assl.md) , elemento de una dimensión de base de datos específica o una dimensión de cubo.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<DimensionPermissions>  
   <DimensionPermission xsi:type="DimensionPermission">...</DimensionPermission> <!-- ancestor: Dimension -->  
   <!-- or -->  
   <DimensionPermission xsi:type="CubeDimensionPermission">...</DimensionPermission> <!-- ancestor: CubePermission -->  
</DimensionPermissions>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Los siguientes son primario válido (o antecesor): pares de tipo de datos:<br /><br /> [Dimensión](../../../analysis-services/scripting/objects/dimension-element-assl.md):[DimensionPermission](../../../analysis-services/scripting/data-type/dimensionpermission-data-type-assl.md)<br /><br /> [CubePermission](../../../analysis-services/scripting/objects/cubepermission-element-assl.md):<br />                        [CubeDimensionPermission](../../../analysis-services/scripting/data-type/cubedimensionpermission-data-type-assl.md)|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-n: Elemento opcional que puede aparecer una vez o más.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[DimensionPermissions](../../../analysis-services/scripting/collections/dimensionpermissions-element-assl.md)|  
  
## <a name="remarks"></a>Comentarios  
 Los elementos correspondientes en el modelo de objetos Objetos de administración de análisis (AMO) son <xref:Microsoft.AnalysisServices.DimensionPermission> y <xref:Microsoft.AnalysisServices.CubeDimensionPermission>.  
  
## <a name="see-also"></a>Vea también  
 [Objetos de &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
