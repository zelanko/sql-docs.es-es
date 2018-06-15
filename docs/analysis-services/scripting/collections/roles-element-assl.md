---
title: Elemento roles (ASSL) | Documentos de Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d246999149c2b23868522fe5d4beb50526993287
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34029486"
---
# <a name="roles-element-assl"></a>Elemento Roles (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Contiene la colección de elementos [Role](../../../analysis-services/scripting/objects/role-element-assl.md) definida bajo el elemento primario.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Database> <!-- or Server -->  
   ...  
   <Roles>  
      <Role>...</Role>  
   </Roles>  
   ...  
</Database>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Ninguno|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Database](../../../analysis-services/scripting/objects/database-element-assl.md), [Server](../../../analysis-services/scripting/objects/server-element-assl.md)|  
|Elementos secundarios|[Rol](../../../analysis-services/scripting/objects/role-element-assl.md)|  
  
## <a name="remarks"></a>Comentarios  
 El elemento **Roles** asociado con un elemento **Server** solamente contiene un rol, denominado Administradores, que representa el rol del administrador del servidor. El rol del administrador del servidor no se puede modificar ni eliminar, ni tampoco los roles adicionales se pueden agregar a la colección.  
  
 El elemento **Roles** asociado a un elemento **Database** contiene los roles definidos para esa base de datos.  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.RoleCollection>.  
  
## <a name="see-also"></a>Vea también  
 [Colecciones de & #40; ASSL & #41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
