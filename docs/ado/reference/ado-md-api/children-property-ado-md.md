---
title: Propiedad Children (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Member::Children
- Children
helpviewer_keywords:
- Children property [ADO MD]
ms.assetid: 61d36468-1ccd-467a-9cb5-17d0bfacc766
author: rothja
ms.author: jroth
ms.openlocfilehash: 7e52923ae428ab7b0e633049594781bd4456f9df
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764396"
---
# <a name="children-property-ado-md"></a>Los elementos secundarios (propiedad, ADO MD)
Devuelve una colección de [miembros](../../../ado/reference/ado-md-api/members-collection-ado-md.md) para la que el [miembro](../../../ado/reference/ado-md-api/member-object-ado-md.md) actual es el elemento primario de la jerarquía.  
  
## <a name="return-values"></a>Valores devueltos  
 Devuelve una colección de **miembros** y es de solo lectura.  
  
## <a name="remarks"></a>Comentarios  
 La propiedad **Children** contiene una colección de **miembros** para la que el **miembro** actual es el elemento primario jerárquico. Los objetos **miembro** de nivel hoja no tienen miembros secundarios en la colección de **miembros** . Esta propiedad solo se admite en los objetos **member** que pertenecen a un objeto [LEVEL](../../../ado/reference/ado-md-api/level-object-ado-md.md) . Se produce un error cuando se hace referencia a esta propiedad desde objetos **member** que pertenecen a un objeto [Position](../../../ado/reference/ado-md-api/position-object-ado-md.md) .  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de miembro (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte también  
 [Propiedad ChildCount (ADO MD)](../../../ado/reference/ado-md-api/childcount-property-ado-md.md)
