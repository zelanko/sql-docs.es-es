---
title: Los elementos secundarios (propiedad, ADO MD) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Member::Children
- Children
helpviewer_keywords:
- Children property [ADO MD]
ms.assetid: 61d36468-1ccd-467a-9cb5-17d0bfacc766
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 630ddeaf83b09dfe502cf07efd7a4185011cff41
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="children-property-ado-md"></a>Los elementos secundarios (propiedad, ADO MD)
Devuelve un [miembros](../../../ado/reference/ado-md-api/members-collection-ado-md.md) colección para la que el actual [miembro](../../../ado/reference/ado-md-api/member-object-ado-md.md) es el elemento primario en la jerarquía.  
  
## <a name="return-values"></a>Valores devueltos  
 Devuelve un **miembros** colección y es de solo lectura.  
  
## <a name="remarks"></a>Comentarios  
 El **elementos secundarios** propiedad contiene un **miembros** colección para la que el actual **miembro** es el principal jerárquico. Nivel de hoja **miembro** objetos no tienen elementos secundarios el **miembros** colección. Esta propiedad solo se admite en **miembro** objetos que pertenecen a un [nivel](../../../ado/reference/ado-md-api/level-object-ado-md.md) objeto. Se produce un error cuando se hace referencia a esta propiedad desde **miembro** objetos que pertenecen a un [posición](../../../ado/reference/ado-md-api/position-object-ado-md.md) objeto.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de miembro (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>Vea también  
 [Propiedad ChildCount (ADO MD)](../../../ado/reference/ado-md-api/childcount-property-ado-md.md)
