---
title: Elemento Miningstructurepermissions (ASSL) | Documentos de Microsoft
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
- MiningStructurePermission Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- MiningStructurePermission
helpviewer_keywords:
- MiningStructurePermission element
ms.assetid: 4ba2bfd2-9003-4eed-8049-a74d452894ea
caps.latest.revision: 43
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 22713569509019e9d0aac30f82c898c73a034fda
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="miningstructurepermission-element-assl"></a>Elemento MiningStructurePermissions (ASSL)
  Define los permisos que los miembros de un [rol](../../../analysis-services/scripting/objects/role-element-assl.md) elemento tiene en un individuo [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<MiningStructurePermissions>  
   <MiningStructurePermission xsi:type="Permission">  
      <AllowDrillthrough>...</AllowDrillthrough>  
  
      <!-- This element also inherits all the child elements listed in Permission -->  
   </MiningStructurePermission>  
</MiningStructurePermissions>  
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
|Elementos primarios|[MiningStructurePermissions](../../../analysis-services/scripting/collections/miningstructurepermissions-element-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.MiningStructurePermission>.  
  
 En [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], el permiso **AllowDrillthrough** se ha ampliado para aplicar a una estructura de minería de datos. Al asignar este permiso a un rol, cualquier usuario que es miembro de ese rol puede consultar directamente la estructura de minería de datos utilizando la sintaxis siguiente:  
  
```  
SELECT <structure column list> FROM <structure>.CASES  
```  
  
 Es más, si **AllowDrillthrough** está habilitado en la estructura de minería de datos y el modelo de minería de datos, los usuarios pueden consultar columnas de estructura que no se incluyeron en el modelo de minería de datos utilizando la sintaxis siguiente:  
  
```  
SELECT StructureColumn('<structure column name>' FROM <model>.CASES  
```  
  
 Por ejemplo, se puede crear un modelo usando solo columnas para clave de cliente, ingresos de cliente y compras de cliente. Utilizando la obtención de detalles, un usuario puede devolver otras columnas de estructura que no se incluyeron en el modelo de minería de datos, como información de contacto del cliente.  
  
 Por consiguiente, para proteger información confidencial o datos personales, debe crear la vista del origen de datos de forma que enmascare los datos personales y conceder el permiso **AllowDrillthrough** en una estructura solo cuando sea necesario.  
  
 Para más información, vea [Consultas de obtención de detalles &#40;minería de datos&#41;](../../../analysis-services/data-mining/drillthrough-queries-data-mining.md).  
  
## <a name="see-also"></a>Vea también  
 <xref:Microsoft.AnalysisServices.MiningModel.AllowDrillThrough%2A>   
 <xref:Microsoft.AnalysisServices.AdomdClient.MiningModel.AllowDrillThrough%2A>   
 [Objetos de &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
