---
title: Elemento roles (ASSL) | Documentos de Microsoft
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
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: f8ced51e40e2804054a0c63368622d2df70f81fc
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199549"
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
  
## <a name="element-characteristics"></a>Características del elemento  
  
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
  
## <a name="remarks"></a>Notas  
 El elemento `Roles` asociado con un elemento `Server` solamente contiene un rol, denominado Administradores, que representa el rol del administrador del servidor. El rol del administrador del servidor no se puede modificar ni eliminar, ni tampoco los roles adicionales se pueden agregar a la colección.  
  
 El elemento `Roles` asociado a un elemento `Database` contiene los roles definidos para esa base de datos.  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.RoleCollection>.  
  
## <a name="see-also"></a>Vea también  
 [Colecciones &#40;ASSL&#41;](collections-assl.md)  
  
  