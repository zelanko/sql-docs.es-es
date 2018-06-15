---
title: Elemento Miningstructurepermissions (ASSL) | Documentos de Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d933d5051a9280d779c23eeb60832aee286dc131
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34032556"
---
# <a name="miningstructurepermission-element-assl"></a>Elemento MiningStructurePermissions (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
 [Objetos de & #40; ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
