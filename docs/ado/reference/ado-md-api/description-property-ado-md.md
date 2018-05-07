---
title: Description (propiedad) (ADO MD) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Member::Description
- Level::Description
- CubeDef::Description
- Hierarchy::Description
- Description
- Dimension::Description
helpviewer_keywords:
- Description property [ADO MD]
ms.assetid: 6d626d35-0bf3-4f24-9934-ad9c9c91273a
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 62938b58b97abfb621cd4e9ea9f9c9e583c124e7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="description-property-ado-md"></a>Description (propiedad) (ADO MD)
Devuelve un texto de explicación del objeto actual.  
  
## <a name="return-values"></a>Valores devueltos  
 Devuelve un **cadena** y es de solo lectura.  
  
## <a name="remarks"></a>Comentarios  
 Para [miembro](../../../ado/reference/ado-md-api/member-object-ado-md.md) objetos, **descripción** se aplica únicamente a medida y fórmulas. **Descripción** devuelve una cadena vacía ("") para todos los demás tipos de miembros. Para obtener más información sobre los distintos tipos de miembros, vea el [tipo](../../../ado/reference/ado-md-api/type-property-ado-md.md) propiedad.  
  
 Esta propiedad solo se admite en **miembro** objetos que pertenecen a un [nivel](../../../ado/reference/ado-md-api/level-object-ado-md.md) objeto. Se produce un error cuando se hace referencia a esta propiedad desde **miembro** objetos que pertenecen a un [posición](../../../ado/reference/ado-md-api/position-object-ado-md.md) objeto.  
  
## <a name="applies-to"></a>Se aplica a  
  
||||  
|-|-|-|  
|[Objeto CubeDef (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)|[Objeto de dimensión (ADO MD)](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)|[Objeto Hierarchy (ADO MD)](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)|  
|[Objeto Level (ADO MD)](../../../ado/reference/ado-md-api/level-object-ado-md.md)|[Objeto de miembro (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)||
