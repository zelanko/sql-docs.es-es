---
title: Elemento Miningstructurepermissions (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- MiningStructurePermission Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MiningStructurePermission
helpviewer_keywords:
- MiningStructurePermission element
ms.assetid: 4ba2bfd2-9003-4eed-8049-a74d452894ea
caps.latest.revision: 43
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2f3789cd5b5b72048b9c9163c11bebf4fe5a77d5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37295495"
---
# <a name="miningstructurepermission-element-assl"></a>Elemento MiningStructurePermissions (ASSL)
  Define los permisos que los miembros de un [rol](role-element-assl.md) tiene elemento individual [MiningStructure](miningstructure-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<MiningStructurePermissions>  
   <MiningStructurePermission xsi:type="Permission">  
      <AllowDrillthrough>...</AllowDrillthrough>  
  
      <!-- This element also inherits all the child elements listed in Permission -->  
   </MiningStructurePermission>  
</MiningStructurePermissions>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|[Permiso](../data-type/permission-data-type-assl.md)|  
|Valor predeterminado|None|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[MiningStructurePermissions](../collections/miningstructurepermissions-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.MiningStructurePermission>.  
  
 En [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], el permiso `AllowDrillthrough` se ha extendido para aplicarse a una estructura de minería de datos. Al asignar este permiso a un rol, cualquier usuario que es miembro de ese rol puede consultar directamente la estructura de minería de datos utilizando la sintaxis siguiente:  
  
```  
SELECT <structure column list> FROM <structure>.CASES  
```  
  
 Es más, si `AllowDrillthrough` está habilitado en la estructura de minería de datos y el modelo de minería de datos, los usuarios pueden consultar columnas de estructura que no se incluyeron en el modelo de minería de datos utilizando la sintaxis siguiente:  
  
```  
SELECT StructureColumn('<structure column name>' FROM <model>.CASES  
```  
  
 Por ejemplo, se puede crear un modelo usando solo columnas para clave de cliente, ingresos de cliente y compras de cliente. Utilizando la obtención de detalles, un usuario puede devolver otras columnas de estructura que no se incluyeron en el modelo de minería de datos, como información de contacto del cliente.  
  
 Por consiguiente, para proteger información confidencial o datos personales, debe crear la vista del origen de datos de forma que enmascare los datos personales y conceder el permiso `AllowDrillthrough` en una estructura solo cuando sea necesario.  
  
 Para más información, vea [Consultas de obtención de detalles &#40;minería de datos&#41;](../../data-mining/drillthrough-queries-data-mining.md).  
  
## <a name="see-also"></a>Vea también  
 <xref:Microsoft.AnalysisServices.MiningModel.AllowDrillThrough%2A>   
 <xref:Microsoft.AnalysisServices.AdomdClient.MiningModel.AllowDrillThrough%2A>   
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  
