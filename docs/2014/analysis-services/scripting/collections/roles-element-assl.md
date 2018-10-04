---
title: Elemento roles (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Roles Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Roles
helpviewer_keywords:
- Roles element
ms.assetid: 4191b7ce-bae4-4200-8550-3904420efafd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 33af9f6cb9ff1d85bdd9de200b66cfb0784fa432
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48168175"
---
# <a name="roles-element-assl"></a>Elemento Roles (ASSL)
  Contiene la colección de elementos [Role](../objects/role-element-assl.md) definida bajo el elemento primario.  
  
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
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Database](../objects/database-element-assl.md), [Server](../objects/server-element-assl.md)|  
|Elementos secundarios|[Rol](../objects/role-element-assl.md)|  
  
## <a name="remarks"></a>Comentarios  
 El elemento `Roles` asociado con un elemento `Server` solamente contiene un rol, denominado Administradores, que representa el rol del administrador del servidor. El rol del administrador del servidor no se puede modificar ni eliminar, ni tampoco los roles adicionales se pueden agregar a la colección.  
  
 El elemento `Roles` asociado a un elemento `Database` contiene los roles definidos para esa base de datos.  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.RoleCollection>.  
  
## <a name="see-also"></a>Vea también  
 [Colecciones &#40;ASSL&#41;](collections-assl.md)  
  
  
